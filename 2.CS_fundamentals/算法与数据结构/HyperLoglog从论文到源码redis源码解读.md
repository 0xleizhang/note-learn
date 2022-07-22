\## ![image.png](1636518496905-706d912a-c8ec-4c22-adbd-2db43acd6f8a.png)

\##

\## 概念

\### 名称

cardinality 集合A中不重复数的个数

[1,2,3,4,5] 基数是5 [1,2,3,4,5,5] 基数仍然是 5

可以理解为：distinct value

如果我们用hash来存储并基数，在数据量很大的时候，hash占用的空间也会线性增长。

\*\*HLL的能力便是能够以很小的空间占用预估很大数据集的基数。\*\*

注意是\*\*预估 (\*\*estimation） 不是精确数

memory\_size= log(log(list\_size))

\### 应用场景
UV user view

直播观看人数 一场直播10个人观看，无论谁重新退出重进多少次 cardinality仍然为10

数据库基数统计

show index from table\_name;

![image.png](1636421359677-6a228a5a-817e-4609-a883-3a849fcb9b52.png)

​

\### redis的用法
ref:[http://redisdoc.com/hyperloglog/pfadd.html](http://redisdoc.com/hyperloglog/pfadd.html)
\> redis> PFADD databases "Redis" "MongoDB" "MySQL"
\> (integer) 1
\> redis> PFCOUNT databases
\> (integer) 3
\> redis> PFADD databases "Redis" \_# Redis 已经存在，不必对估计数量进行更新\_
\> (integer) 0
\> redis> PFCOUNT databases \_# 元素估计数量没有变化\_
\> (integer) 3
\> redis> PFADD databases "PostgreSQL" \_# 添加一个不存在的元素\_
\> (integer) 1
\> redis> PFCOUNT databases \_# 估计数量增一\_
\> 4

\## 论文

P. Flajolet, Éric Fusy, O. Gandouet, and F. Meunier. Hyperloglog: The analysis of a near-optimal cardinality estimation algorithm. 2007年

提出者 法国人,作者名字首字母PF 所以redis命令为PFADD ，设计初衷主要假象的是解决网络攻击中的问题

在此之前已有loglog算法，hyperloglog是对loglog（2003年）的改良

在此之后有hyperloglog++ Google改良版

![image.png](1636339175099-754ac735-440a-4f23-8a52-08e91d2afad5.png) 第一作者

Google实践、改良 2013年

Heule, Nunkesser, Hall: HyperLogLog in Practice: Algorithmic Engineering of a State of The Art Cardinality Estimation Algorithm.

\### 数学原理
伯努利实验的应用：

hash结果64位，取后50位，每一位是独立的可能为0可能为1

连续为0的个数表述上等同于第一次出现1的位

​

掷硬币，10次一组，一组称之为一次伯努利过程

一个hash(value)=64bit 等同为一次伯努利过程。

![image.png](1636362229195-26ef1fda-ba40-4086-beea-616806e04a86.png)

两个数学原理：

![](https://cdn.nlark.com/yuque/\_\_latex/c406b0be9f1631b578dd0309c5ff11e1.svg#card=math&code=2%5Ek%20%3D%20N%20&id=Ifl8u)

​

​

m=桶数

调和平均值

const常量

![image.png](1636380125556-4a6a0cf3-a136-48b6-b08f-77208f2427b5.png)

​

​

​

\## redis源码实现

\##

\### 观其大要
[src/hyperloglog.c](https://github.com/yahoo/redislite/blob/master/redis.submodule/src/hyperloglog.c)

注释

命令处理

count 过程

sparse稀疏处理方式实现：set ,add ,histo

dense 密集处理方式实现：set ,add ,histo

inline ：murmurHash64A

宏

常量

\### 带着问题读源码
数据结构是怎么样的？

Add到Count的处理过程？

有哪些背景知识？

\### 背景知识
如果阅读源码过程中设计的其他的知识，先把其了解清楚。

1 伯努利实验｜伯努利过程 ｜ 伯努利分布

![image.png](1636380486747-46c49759-e96b-44f9-8669-6fe4830555bc.png)

2 hash算法

​

3 C语法：宏，位运算

\### 存储过程
hash=>64bit

取前14位作为index 找到对应的桶 所以需要2^14 个桶

取第一个出现1的位作为值，如果值大于旧值更新，位数最大值是50 所以用6bit能够存储

​

count > 32 spare转换成dense实现方式

\### 存储结构

一图胜千言：[miro-link](https://miro.com/app/board/o9J\_lkCGlmo=/?invite\_link\_id=721726249386)

 ![](https://cdn.nlark.com/yuque/\_\_latex/c406b0be9f1631b578dd0309c5ff11e1.svg#card=math&code=2%5Ek%20%3D%20N%20&id=WKotp) 基于以上数学原理的了解，实际上需要存储的是数字 k

​

为了解决误差问题，分成了多个桶，其中多桶解决误差问题，在其他诸如\`count min sketch\`中也有见到。

2^14 个桶

每个桶存储6bit 存储能表示的最大值=2^6 = 64 完全能够存下50。

计算机中最小存取单位是1byte=8bit，redis为了极致利用内存，会根据offset判断是否取上一个或下一个进行位运算，得到k。

取值场景有:

\*\*[6,2][4,4][2,6][6,2][4,4][2,6]\*\*[6,2][4,4][2,6][6,2][4,4][2,6]

为什么用int8[8]数组来缓存cardinality值？，猜测是历史原因：

![image.png](1636435255878-0ccc3b15-58ab-4079-88a9-07ff985b5cfe.png)

\### 取值过程
套公式，调和平均值

论文：[https://arxiv.org/abs/1702.01284](https://arxiv.org/abs/1702.01284)

\###
​

​

​

​

\## 其他语言实现

go:[https://github.com/axiomhq/hyperloglog](https://github.com/axiomhq/hyperloglog)

​

​

output: [https://www.bilibili.com/video/BV1Wq4y1k7Dy/](https://www.bilibili.com/video/BV1Wq4y1k7Dy/)

05:23 论文及理论部分

26:43 源码解读