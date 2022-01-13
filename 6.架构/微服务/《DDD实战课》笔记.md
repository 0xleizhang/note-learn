DDD is架构设计方法

微服务 is 架构风格

\# 领域
核心域、通用域和支撑域

不同公司不同业务核心域是不同的

战略设计，战术设计

\## 领域建模
战略设计

为了：

他们的：

这个：

是一个：

它可以：

而不像：

我们的产品：

![](https://cdn.nlark.com/yuque/0/2020/jpeg/290656/1595906561278-e2e0f7af-d4a2-41aa-9f01-22acadfec606.jpeg#align=left&display=inline&height=1176&margin=%5Bobject%20Object%5D&originHeight=1176&originWidth=1680&size=0&status=done&style=none&width=1680)

战术设计

领域对象的整理：

![](https://cdn.nlark.com/yuque/0/2020/jpeg/290656/1595906646200-aa2c9795-0bc4-4be0-9baa-8b89d95b3cbe.jpeg#align=left&display=inline&height=994&margin=%5Bobject%20Object%5D&originHeight=994&originWidth=1284&size=0&status=done&style=none&width=1284)

层，领域模型，聚合，领域对象，领域类型，对应类，对应方法，对应包

\# bound context 上下文边界
通用语言内部沟通统一语言

领域边界 is bound context

\# 实体、值对象
实体 is 充血模型

实体 has id

实体use id to 追踪

值对象 is 属性集合 is vo

实体 can 嵌套 值对象 Person::Address

\# 聚合、聚合根
一类实体\- 聚合 \- 包

聚合根 is public 发言人

\# 领域事件
识别领域事件：：“如果发生……，则……”“当做完……的时候，请通知……”“发生……时，则……”

解耦

削峰填谷

最终一致

\# 分层
目标：解耦

不跨层调用

![](assert/1595901134939-c6b52a21-f5c0-49b1-b54e-fc2b75ccac2c.png)

\# 架构模型

\## 整洁架构（ 洋葱架构）
![](assert/1595901319777-d95fbae5-bfce-4ecb-9a66-fa479bbfb16f.png)

\## 六边形架构（端口适配器架构）
![](assert/1595901356672-375d7034-b8d1-41a4-8820-9c4f8dd11ed8.png)

\## DDD分层架构

\## 企业级中台微服务
Backend for Frontends

![](assert/1595901447899-730295e0-8cd4-49e1-a29a-76f314495415.png)

\# 中台
业务中台的建设可采用领域驱动设计方法，通过领域建模，将可复用的公共能力从各个单体剥离，沉淀并组合，采用微服务架构模式，建设成为可共享的通用能力中台。

\*\*数据中台的主要目标是打通数据孤岛，实现业务融合和创新。\*\*

\*\*![](assert/1595906283680-a18b3a60-9456-4df0-83df-837643c4c246.png)

\# 代码模型

[https://github.com/ouchuangxin/leave-sample](https://github.com/ouchuangxin/leave-sample)

接口层有assembler负责DTO 和DO （领域对象）的互相转化

\# 其他相关

\## 前端
微前端架构