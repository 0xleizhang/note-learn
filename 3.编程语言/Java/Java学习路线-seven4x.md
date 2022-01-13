80年代以来人类计算机软件行业发展最辉煌的几年，很多都积累在了Java生态中，见：[java知识全图](https://www.oracle.com/topics/technologies/newtojava-java-technology-concept-map.html).

虽然Java生态很多知识，一部分很多都是过时废弃的，一部分是专有领域性的，如果要达到一个胜任基本的后端工作（增删改查+）要\*\*学的东西不多\*\*。

Java发展这么多年了教程数不胜数，现代核心问题不是缺少教程而是如何\*\*识别出好教程\*\*

适用读者：有其他语言开发经验的程序员，迁移到Java领域并快速上手开发工作。文档列出了路径的关键概念及链接。

编程是一个实践性很强的学科，需要\*\*大量的练习\*\*。

先会用，暂不深入

\# 阶段1 菜鸟教程 tutorial

\### java语法
 弄懂语法，if else 循环，接口 类 ，面向对象，

推荐资料：[https://www.runoob.com/java/java-tutorial.html](https://www.runoob.com/java/java-tutorial.html)

更推荐官方版：[https://docs.oracle.com/javase/tutorial/](https://docs.oracle.com/javase/tutorial/)

\### 数据库基础

mysql教程：[https://www.runoob.com/mysql/mysql-tutorial.html](https://www.runoob.com/mysql/mysql-tutorial.html)

\### git基础

[https://git-scm.com/book/zh/v2](https://git-scm.com/book/zh/v2)

\# 1到3个月之后

\# 阶段2 tool,framework,library

\## ⚠️以终为始(以项目为导向)
前面的三部分知识都可以进行独立的练习，后面的学习如果只停留再听理论，学习效果会很差

这里就要假设做一个项目为例来看展学习。

比如：用Java做一个博客的后端（增删改查，登陆授权验证)等等

或者面向offer学习，多看一看大公司的JD

\## 开发工具

\### idea
[https://www.jetbrains.com/idea/](https://www.jetbrains.com/idea/)

\### maven

包管理器，类比其他语言的包管理

常用的两三个命令，基本会用就行

资料：

[https://www.runoob.com/maven/maven-tutorial.html](https://www.runoob.com/maven/maven-tutorial.html)

[https://www.liaoxuefeng.com/wiki/1252599548343744/1309301146648610](https://www.liaoxuefeng.com/wiki/1252599548343744/1309301146648610)

\#

\## 开发框架

\### springboot with spring mvc
\*\*先明确概念，提纲挈领，以实现目标为参照 抓重点内容\*\*

\*\*

springmvc 是经典的mvc设计模式的框架

类似ruby的rails

代替了过时的structs2

springboot是为了解决spring开发集成的复杂性，通过一些机制能够很方便的集成其他开发组件

比如集成redis,消息队列kafka等

官方：[https://spring.io/guides/gs/serving-web-content/](https://spring.io/guides/gs/serving-web-content/)

[https://www.baeldung.com/spring-mvc-tutorial](https://www.baeldung.com/spring-mvc-tutorial)

[https://blog.didispace.com/spring-boot-learning-2x/](https://blog.didispace.com/spring-boot-learning-2x/)

视频教程：[bilibili](https://search.bilibili.com/all?keyword=spring%20boot%20%E6%95%99%E7%A8%8B&from\_source=nav\_search\_new)

\### mybatis

[https://mybatis.org/mybatis-3/zh/index.html](https://mybatis.org/mybatis-3/zh/index.html)

[https://wiki.jikexueyuan.com/project/mybatis-in-action/](https://wiki.jikexueyuan.com/project/mybatis-in-action/)

mybatis 与spring集成

[http://mybatis.org/spring-boot-starter/mybatis-spring-boot-autoconfigure/](http://mybatis.org/spring-boot-starter/mybatis-spring-boot-autoconfigure/)

\### 工具库
[https://www.hutool.cn/](https://www.hutool.cn/)

\## ⚠️ 就是这些
以上学会就能完成基本的开发了，需要一定的练习

做出项目之前可能会接触到以下方面，但是不懂也没关系

1\. logging framework 日志系统
1\. junit 单元测试

一个有经验的程序员包装一下简历，背一些面试题可以能以高级职称入职了

\# 3~9个月之后

\# 阶段3 熟练度
[语言核心](https://docs.oracle.com/javase/specs/jls/se8/html/index.html)

标准库，集合 ，反射

juc 并发编程

\*\*会搜-会抄 复制粘贴（各种开发脚手架）\*\*

\# 阶段4 广度

\### 常用中间件
redis [http://redisdoc.com/](http://redisdoc.com/)

[kafka](https://kafka.apache.org/documentation/)

nginx [http://www.nginx.cn/doc/](http://www.nginx.cn/doc/)

微服务开发框架：[https://dubbo.apache.org/zh/](https://dubbo.apache.org/zh/)

[https://github.com/alibaba/spring-cloud-alibaba/blob/master/README-zh.md](https://github.com/alibaba/spring-cloud-alibaba/blob/master/README-zh.md)

分库分表：[http://shardingsphere.apache.org/index\_zh.html](http://shardingsphere.apache.org/index\_zh.html)

Linux基础命令 [https://linuxtools-rst.readthedocs.io/zh\_CN/latest/base/index.html](https://linuxtools-rst.readthedocs.io/zh\_CN/latest/base/index.html)

apache:[https://projects.apache.org/projects.html?category](https://projects.apache.org/projects.html?category)

\# 1~3年之后

\# 阶段5 深度
理解 spring-core

深入 JVM：[https://docs.oracle.com/javase/specs/jvms/se8/html/](https://docs.oracle.com/javase/specs/jvms/se8/html/)

JSR:[https://github.com/mercyblitz/jsr](https://github.com/mercyblitz/jsr) [ JSR-133内存模型](https://www.infoq.cn/minibook/java\_memory\_model)

数据库原理 ，索引及优化

官方手册： [https://dev.mysql.com/doc/refman/8.0/en/](https://dev.mysql.com/doc/refman/8.0/en/)

《mysql 权威指南》

Linux I/O 网络 协议

分布式系统：

\# 一段时间之后

\# 阶段五 架构...
[https://time.geekbang.org/column/intro/100006601](https://time.geekbang.org/column/intro/100006601)

《重构》 《设计模式》 《架构简洁之道》

 云原生 k8s ...

\#

\#

\# 核心总结

[The Java™ Tutorials](https://docs.oracle.com/javase/tutorial/)

[The Java® Language Specification](https://docs.oracle.com/javase/specs/jls/se8/html/index.html)

[The Java® Virtual Machine Specification](https://docs.oracle.com/javase/specs/jvms/se8/html/)

\## 不要学哪些
不要学eclipse

\_jsp\_

\_struct2\_

\_hibernate\_

\_shiro\_

\_

可以学一些培训机构的视频，不要完全看培训机构的视频，原因：\*\*培训机构是面向面试的学习，\*\*涉及到的底层原理当时你可能没法理解

\## 其他资料：

[搜索引擎](https://blog.csdn.net/qq\_34033853/article/details/79311303)

[https://s.geekbang.org/](https://s.geekbang.org/)

[https://wiki.jikexueyuan.com/list/java/](https://wiki.jikexueyuan.com/list/java/)

[https://www.journaldev.com/](https://www.journaldev.com/)

[https://howtodoinjava.com/](https://howtodoinjava.com/)

[https://gitee.com/seven4q/knowledge/invite\_link?invite=9a8ad1489082c3200f2289180d35679537817bc90a6371d6b7993663152babc5348c0f662159463a6121c5559972f7e3](https://gitee.com/seven4q/knowledge/invite\_link?invite=9a8ad1489082c3200f2289180d35679537817bc90a6371d6b7993663152babc5348c0f662159463a6121c5559972f7e3)