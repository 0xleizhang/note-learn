作用：
\> 类似java中的JMS 将指标信息通过http端口暴露出来，prometheus exporter能够轮询保存到pro库中，用作后续的监控和告警

\# 数据类型

gauge 瞬时值类型

histogram 直方图 能够做出

Counter 计数

\# 使用步骤
1 通过 prometheus.NewGauge创建

2 prometheus.MustRegister(diskFree) 注册Collector

3 服务通过endpoint暴露metrics
\`\`\`
 metrics.ExposeMetrics("ghproxy", config.PushGateway{
 Endpoint: o.pushGateway,
 Interval: &metav1.Duration{
 Duration: o.pushGatewayInterval,
 },
 ServeMetrics: o.serveMetrics,
 }, o.instrumentationOptions.MetricsPort)
\`\`\`
4 通过set更新值
\`\`\`
diskFree = prometheus.NewGauge(prometheus.GaugeOpts{
 Name: "ghcache\_disk\_free",
 Help: "Free gb on github-cache disk",
})

diskFree.Set(float64(bytesFree) / 1e9)

\`\`\`