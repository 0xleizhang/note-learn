整体架构

​

![image.png](1640922442743-45fd5ca3-9e01-48ae-b336-f9b4710ae800.png)

\# prometheus部分

告警配置示例
\`\`\`sql
groups:
\- name: example
 rules:
 \- alert: mysql\_uptime
 expr: mysql:server\_status:uptime < 30
 for: 10s
 labels:
 level: "CRITICAL"
 annotations:
 detail: 数据库运行时间
\`\`\`

\- inactive：没有触发阈值
\- pending：已触发阈值但未满足告警持续时间 expr = ture && < for
\- firing：已触发阈值且满足告警持续时间 expr=true && for > 10

​

scrape\_interval 采集周期 evaluation\_interval 计算周期

​

 resolve 消息标记解决

​

​

​

\# alter-manager部分
![image.png](1640922805051-da63a6fc-be7a-4172-b5a2-cd34400ecc05.png)

​

处理告警流程

​

收敛：

group 分组 合并

inhibitor 抑制 A告警必然导致B 抑制B

silencer 静默 告警是可预期的，夜里跑批负载变高

​

延迟：Dedup阶段

group\_by

group\_wait 分组等待时间 用于合并

group\_interval 分组尝试再次发送时间

Repeat\_interval 分组内发送相同告警间隔

​

​