


以下组件
服务端 ：server ,handler  

客户端：Transport。RoundTripper 


server 构建需要一个Handler

```go
type Handler interface {  
   ServeHTTP(ResponseWriter, *Request)  
}
```


几种方式：

handlerFunc
serveMux


ReverseProxy 也是一个Handler
```
type ReverseProxy struct {  
 // Director must be a function which modifies
 // the request into a new request to be sent 
 // using Transport. Its response is then copied  
 // back to the original client unmodified.
 // Director must not access the provided Request
 // after returning. 
 Director func(*http.Request)  
  
 // The transport used to perform proxy requests.  
 // If nil, http.DefaultTransport is used.
 Transport http.RoundTripper
```


通过`httputil.NewSingleHostReverseProxy(upstreamURL)` 创建ReverseProxy

transport 为roundtripper   
roundtripper 类似于调用链模式，外层封装内层，一般先调用内层

```
type RoundTripper interface {  
 RoundTrip(*Request) (*Response, error)  
}

```


被包装层次
http.DefaultTransport -> apptokenequalizer -> upstreamTransport -> throttlingTransport 限流 -> partitioningRoundTripper  redis分区

调用顺序相反
