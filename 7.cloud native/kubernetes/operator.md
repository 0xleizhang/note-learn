\## 如何理解operator
有一些应用的部署用k8s自带的deployment等对象玩不转了，比如一些分布式应用Kafka之类

这时候需要提供一种自定义扩展能力，通过Custom resource Defind (CRD)+operator

operator可以理解是操作k8s api的客户端

需要自己写代码实现Control控制器

高级操作=>低级操作 体现了概念的抽象 体现了应用程序的封装

\## 开发生命流程图
![image.png](1624938483363-3c2c528e-e3d2-4b12-9723-1aef6ac2a17f.png)