
spring framework 下的 [Scheduling](https://docs.spring.io/spring-framework/docs/current/reference/html/integration.html#scheduling) 是一层抽象


具体实现可以是：jdk Timer ,[Quartz](https://docs.spring.io/spring-boot/docs/current/reference/html/io.html#io.quartz) ,[awaitility](https://spring.io/guides/gs/scheduling-tasks/)


分布式任务：
[shedlock](https://github.com/lukas-krecan/ShedLock) , jobRunr
支持分片 xxl-job,schedulerX2.0