# 关系

## 1 依赖关系 Dependency

A --> B

表现在代码层面，为类B作为参数被类A在某个method方法中使用；

![image.png](assert/1637764217895-1c9f334f-8bc7-4759-81c9-5a2b9f998c9c.png)

​

## 2 关联关系 Association

表现在代码层面，为被关联类B以类属性的形式出现在关联类A中，也可能是关联类A引用了一个类型为被关联类B的全局变量；

![image.png](assert/1637764247292-013975ba-1b24-4b13-bba0-59f0239c80cd.png)

## 3 聚合（Aggregation）
关联关系特例

表现在代码层面，和关联关系是一致的，只能从语义级别来区分；

 **has-a关系**

 计算机 has cpu 内存 硬盘

![image.png](assert/1637764325711-624915e8-b457-49d2-95bb-e7678a539200.png)

​

## 4 组合（复合，Composition）

关联关系特例

**contains-a 关系**

![image.png](assert/1637764405234-ad7f6544-e0e2-4c5d-8655-286738eba553.png)

> 他同样体现整体与部分间的关系，但此时整体与部分是不可分的，整体的生命周期结束也就意味着部分的生命周期结束；比如你和你的大脑

## 5 泛化（Generalization）

类实线 接口虚线

![image.png](assert/1637764071818-9cb7b28f-ee4f-47c0-a43e-fb28c8b2d045.png)

![image.png](assert/1637764080921-6665b657-b40f-49de-b8d9-f6164fb58580.png)