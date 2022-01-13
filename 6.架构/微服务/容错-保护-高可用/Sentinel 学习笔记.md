solgan:

Sentinel 是面向分布式服务架构的流量控制组件，主要以流量为切入点，从限流、流量整形、熔断降级、系统自适应保护、热点防护等多个维度来帮助业务保障微服务的稳定性。

![](https://raw.githubusercontent.com/alibaba/Sentinel/master/doc/image/sentinel-opensource-eco-landscape-en.png#align=left&display=inline&height=1924&margin=%5Bobject%20Object%5D&originHeight=1924&originWidth=3355&status=done&style=none&width=3355)

\# 资源
开源文档

[https://github.com/alibaba/Sentinel/wiki/%E4%BB%8B%E7%BB%8D?spm=a1zco.sentinel.0.0.544d7a11HMlots](https://github.com/alibaba/Sentinel/wiki/%E4%BB%8B%E7%BB%8D?spm=a1zco.sentinel.0.0.544d7a11HMlots)

云产品文档

[https://help.aliyun.com/document\_detail/167568.html?spm=a2c4g.11186623.6.633.70a62fb7qPanU7](https://help.aliyun.com/document\_detail/167568.html?spm=a2c4g.11186623.6.633.70a62fb7qPanU7)

awesome

[https://github.com/sentinel-group/sentinel-awesome](https://github.com/sentinel-group/sentinel-awesome)

use nacos as data source

[http://blog.didispace.com/spring-cloud-alibaba-sentinel-2-1/](http://blog.didispace.com/spring-cloud-alibaba-sentinel-2-1/)

[https://juejin.im/post/5ce3b5faf265da1b5d577fca](https://juejin.im/post/5ce3b5faf265da1b5d577fca)

\# 基本概念

\## 保护
限流

![image.png](1595986437835-df1c70bc-aac2-4dd7-8efc-568d3588aff2.png)

![image.png](1595986777333-dadc5c0a-2234-465b-a99b-80f86f56beb8.png)

降级

![image.png](1595986409677-46e780f9-08b9-412a-8586-c0ec4300ea39.png)

热点保护

![image.png](1595986494283-61777ae1-e840-44d2-b20a-453624fc952f.png)

sentinel 如何区分调用者应用

\## 术语

\### 簇点 切入点
 表示程序中受Sentinel监控的一个切入点类 似AOP切入点的概念。

\### 资源名
 每个簇点使用资源名进行代表。资源名是有业 务语义的字符串，比如方法签名，或者URL地 址等。

\### 簇点链路
 有层次关系的簇点组成的链路，类似方法的调 用链。

\### 链路入口
在进入切入点之前，声明链路路口来区分属于哪一条特定链路，Sentinel 默认支持的链路路口有 Web 和 HSF provider 等。只有声明了链路入口后续调用的切入点才会纳入链路管理。

\### 孤儿结点(默认节点）
未纳入链路管理的切入点节点

\## 整体结构
![](1595986055119-73315292-ed2d-4917-8d6f-41cd9a487a10.png)

\# 接入

\## 手动
\`\`\`
Entry entry = null;
// 务必保证 finally 会被执行
try {
 // 资源名可使用任意有业务语义的字符串，注意数目不能太多（超过 1K），超出几千请作为参数传入而不要直接作为资源名
 // EntryType 代表流量类型（inbound/outbound），其中系统规则只对 IN 类型的埋点生效
 entry = SphU.entry("自定义资源名");
 // 被保护的业务逻辑
 // do something...
} catch (BlockException ex) {
 // 资源访问阻止，被限流或被降级
 // 进行相应的处理操作
} catch (Exception ex) {
 // 若需要配置降级规则，需要通过这种方式记录业务异常
 Tracer.traceEntry(ex, entry);
} finally {
 // 务必保证 exit，务必保证每个 entry 与 exit 配对
 if (entry != null) {
 entry.exit();
 }
}
\`\`\`

\# 控制台
它提供机器发现以及健康情况管理、监控（单机和集群），规则管理和推送的功能

\## 启动控制台

\## 客户端接入控制台
1 引入transport jar包

2 启动参数指定控制台ip端口 -Dcsp.sentinel.dashboard.server=consoleIp:port

\- 客户端URL被访问过才能在控制台看到对应的资源

\# 限流规则配置

\# 降级规则配置

\# 热点规则配置

\# 授权规则配置

\# 系统保护规则配置

\# 工作原理

责任链模式

滑动窗口算法 令牌桶算法

限流表现=getEntry 抛异常