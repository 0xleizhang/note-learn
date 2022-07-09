---
isbn: 9787111349662
category: 计算机-编程设计
lastReadDate: 2022-02-20T00:00:00.000Z
doc_type: weread-highlights-reviews
bookId: '603093'
author: 周志明
cover: 'https://wfqqreader-1252317822.image.myqcloud.com/cover/93/603093/t7_603093.jpg'
reviewCount: 3
noteCount: 0
---
# 元数据
> [!abstract] 深入理解Java虚拟机：JVM高级特性与最佳实践
> - ![ 深入理解Java虚拟机：JVM高级特性与最佳实践|200](https://wfqqreader-1252317822.image.myqcloud.com/cover/93/603093/t7_603093.jpg)
> - 书名： 深入理解Java虚拟机：JVM高级特性与最佳实践
> - 作者： 周志明
> - 简介： 作为一位Java程序员，你是否也曾经想深入理解Java虚拟机，但是却被它的复杂和深奥拒之门外？没关系，本书极尽化繁为简之妙，能带领你在轻松中领略Java虚拟机的奥秘。本书是近年来国内出版的唯一一本与Java虚拟机相关的专，也是唯一一本同时从核心理论和实际运用这两个角度去探讨Java虚拟机的作，不仅理论分析得透彻，而且书中包含的典型案例和最佳实践也极具现实指导意义。
> - 出版时间 2011-07-01 00:00:00
> - ISBN： 9787111349662
> - 分类： 计算机-编程设计
> - 出版社： 机械工业出版社

# 高亮划线

## 第13章 线程安全与锁优化


- 📌 调用。这点并不容易做到，在大多数场景中，我们都会将这个定义弱化一些，如果把“调用这个对象的行为”限定为“单次调用”，这个定义的其他描述也能够成立的话，我们就可以称它是线程安全的了，为什么要弱化这个定义 ^603093-17-1925
    - ⏱ 2017-11-01 22:50:15 
# 读书笔记

## 第五部分 高效并发

### 划线评论
- 📌 for (int i = 0; i < THREADS_COUNT; i++) {￼               threads[i] = new Thread(new Runnable() {￼                   @Override￼                   public void run() {￼                       for (int i = 0; i < 10000; i++) {￼                             increase();￼                       }￼                   }￼               });￼               threads[i].start();￼         } ￼         // 等待所有累加线程都结束￼         while (Thread.activeCount() > 1)￼     }￼ }￼             Thread.yield(); ￼         System.out.println(race);
这段代码发起了20个线程，每个线程对race变量进行10000次自增操作，如果这段代码能够正确并发的话，最后输出的结果应该是200000。  ^13176609-71muZK68l
    - 💭 thread.activeCount 和jvm有关，这行会有死循环
    - ⏱ 2018-08-02 11:25:55

### 划线评论
- 📌 for (int i = 0; i < THREADS_COUNT; i++) {￼               threads[i] = new Thread(new Runnable() {￼                   @Override￼                   public void run() {￼                       for (int i = 0; i < 10000; i++) {￼                             increase();￼                       }￼                   }￼               });￼               threads[i].start();￼         } ￼         // 等待所有累加线程都结束￼         while (Thread.activeCount() > 1)￼     }￼ }￼             Thread.yield(); ￼         System.out.println(race);
这段代码发起了20个线程，每个线程对race变量进行10000次自增操作，如果这段代码能够正确并发的话，最后输出的结果应该是200000。  ^13176609-71muoznyY
    - 💭 这段代码有误，i变量声明与括弧对不上
    - ⏱ 2018-08-02 11:16:45

### 划线评论
- 📌 经过长时间的验证和修补，在JDK 1.5（实现了JSR-133￼）发布后，Java的内存模型就已经成熟和完善起来了。
12.3.1 主内存与工作内存
Java内存模型的主要目标是定义程序中各个变量的访问规则，即在虚拟机中将变量存储到内存和从内存中取出变量这样的底层细节。此处的变量（Variable）与Java编程中所说的变量略有区别，它包括了实例字段、静态字段和构成数组对象的元素，但是不包括局部变量与方法参数，因为后者是线程私有的￼，不会被共享，自然就不存在竞争问题。  ^13176609-70KsOO6fp
    - 💭 想到了学数学的知识点依赖性，不懂这里的主内存和工作内存就懂不了后面的volatile
    - ⏱ 2018-07-08 11:19:12
   
# 本书评论
