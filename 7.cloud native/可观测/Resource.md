
 
 
* OpenTelemetry
* OpenTracing
* OpenCensus
* OpenMetrics prometheus
* OpenObservability 并不存在


选手们

1. old school. APM
2. prometheus
3. elastic [ELK](https://www.elastic.co/what-is/elk-stack)




>OpenTracing 规范公布后，几乎所有业界有名的追踪系统，譬如 Zipkin、Jaeger、SkyWalking 等都很快宣布支持 OpenTracing，但谁也没想到的是，Google 自己却在此时出来表示反对，并提出了与 OpenTracing 目标类似的 OpenCensus 规范，随后又得到了巨头 Microsoft 的支持和参与。OpenCensus 不仅涉及追踪，还把指标度量也纳入进来；内容上不仅涉及规范制定，还把数据采集的探针和收集器都一起以 SDK（目前支持五种语言）的形式提供出来。

>OpenTracing 和 OpenCensus 迅速形成了可观测性的两大阵营，一边是在这方面深耕多年的众多老牌 APM 系统厂商，另一边是分布式追踪概念的提出者 Google，以及与 Google 同样庞大的 Microsoft。对追踪系统的规范化工作，并没有平息厂商竞争的混乱，反倒是把水搅得更加浑了。

>正当群众们买好西瓜搬好板凳的时候，2019 年，OpenTracing 和 OpenCensus 又忽然宣布握手言和，它们共同发布了可观测性的终极解决方案[OpenTelemetry](https://opentelemetry.io/)，并宣布会各自冻结 OpenTracing 和 OpenCensus 的发展。OpenTelemetry 野心颇大，不仅包括追踪规范，还包括日志和度量方面的规范、各种语言的 SDK、以及采集系统的参考实现，它距离一个完整的追踪与度量系统，仅仅是缺了界面端和指标预警这些会与用户直接接触的后端功能，OpenTelemetry 将它们留给具体产品去实现，勉强算是没有对一众 APM 厂商赶尽杀绝，留了一条活路。


[**https://www.gartner.com/reviews/market/application-performance-monitoring**](https://www.gartner.com/reviews/market/application-performance-monitoring)

  

[**https://www.g2.com/categories/application-performance-monitoring-apm**](https://www.g2.com/categories/application-performance-monitoring-apm)

  

[**https://www.g2.com/categories/observability-solution-suites**](https://www.g2.com/categories/observability-solution-suites)

  
https://lib.jimmysong.io/opentelemetry-obervability/architectural-overview/
  

[**https://docs.datadoghq.com/tracing/setup_overview/open_standards/#pagetitle**](https://docs.datadoghq.com/tracing/setup_overview/open_standards/#pagetitle)

  

[**https://time.geekbang.org/column/article/346235**](https://time.geekbang.org/column/article/346235)

   
[**http://icyfenix.cn/distribution/observability/tracing.html#%E8%BF%BD%E8%B8%AA%E8%A7%84%E8%8C%83%E5%8C%96**](http://icyfenix.cn/distribution/observability/tracing.html#%E8%BF%BD%E8%B8%AA%E8%A7%84%E8%8C%83%E5%8C%96)

  

[**http://icyfenix.cn/immutable-infrastructure/container/history.html#%E5%B0%81%E8%A3%85%E9%9B%86%E7%BE%A4%EF%BC%9Akubernetes**](http://icyfenix.cn/immutable-infrastructure/container/history.html#%E5%B0%81%E8%A3%85%E9%9B%86%E7%BE%A4%EF%BC%9Akubernetes)

  

[**https://www.oneapm.com/**](https://www.oneapm.com/)

  

**https://aws.amazon.com/cn/products/management-and-governance/use-cases/monitoring-and-observability/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc&blog-posts-cards.sort-by=item.additionalFields.createdDate&blog-posts-cards.sort-order=desc**


# famous tracing 
https://zipkin.io/
https://www.jaegertracing.io/
skywalking tracing之后又了log metrics
https://github.com/grafana/tempo


# famous metrics
https://github.com/elastic/apm-server


# logs 
Beats vs fluentd




