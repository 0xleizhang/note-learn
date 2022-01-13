\# JVM

\### 运行时数据区

[2.5.1. The \`pc\` Register](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-2.html#jvms-2.5.1) 类似于PC计数器程序指令 每个线程一个

[2.5.2. Java Virtual Machine Stacks](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-2.html#jvms-2.5.2) 栈 每个线程一个

[2.5.3. Heap](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-2.html#jvms-2.5.3) 堆 对象分配 全部线程共享

[2.5.4. Method Area](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-2.html#jvms-2.5.4) 存储类信息，全部线程共享

[2.5.5. Run-Time Constant Pool](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-2.html#jvms-2.5.5) 运行时常量池，类似于汇编数据段 逻辑上的，从Method Area区分配

[2.5.6. Native Method Stacks](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-2.html#jvms-2.5.6) 本地方法区，c代码的stack