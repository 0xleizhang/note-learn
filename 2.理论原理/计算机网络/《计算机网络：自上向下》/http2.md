ref:

[https://developers.google.com/web/fundamentals/performance/http2](https://developers.google.com/web/fundamentals/performance/http2)

google's SPDY协议-标准化>http2

基于tcp

google's QUIC-标准化>http/3

基于udp

\## 特点

二进制分帧层：指的是位于套接字接口与应用可见的高级 HTTP API 之间一个经过优化的新编码机制

![image.png](assert/1616991972969-15e58a28-7dd1-4d77-903f-20eb548c74d5.png)

请求与响应复用

将 HTTP 消息分解为独立的帧，交错发送，然后在另一端重新组装是 HTTP 2 最重要的一项增强

请求优先级

头部压缩

服务端推送

一次请求，多个点响应

![image.png](assert/1616991210980-53588142-764d-4053-99b8-31442af2f952.png)

\##

\## Chrome离线通知