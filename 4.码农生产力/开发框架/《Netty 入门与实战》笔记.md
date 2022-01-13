[https://juejin.im/book/5b4bc28bf265da0f60130116](https://juejin.im/book/5b4bc28bf265da0f60130116)

[https://github.com/lightningMan/flash-netty.git](https://github.com/lightningMan/flash-netty.git)

![image.png](1595984690138-15723c4f-454d-4d01-ba31-d057ae1d288f.png)

\# IO类型代码对比

\## BIO
\`\`\`java
/\\*\\*
 \\* @author 闪电侠
 \*/
public class IOServer {
 public static void main(String[] args) throws Exception {

 ServerSocket serverSocket = new ServerSocket(8000);

 // (1) 接收新连接线程
 new Thread(() -> {
 while (true) {
 try {
 // (1) 阻塞方法获取新的连接
 Socket socket = serverSocket.accept();

 // (2) 每一个新的连接都创建一个线程，负责读取数据
 new Thread(() -> {
 try {
 int len;
 byte[] data = new byte[1024];
 InputStream inputStream = socket.getInputStream();
 // (3) 按字节流方式读取数据
 while ((len = inputStream.read(data)) != -1) {
 System.out.println(new String(data, 0, len));
 }
 } catch (IOException e) {
 }
 }).start();

 } catch (IOException e) {
 }

 }
 }).start();
 }
}

/\\*\\*
 \\* @author 闪电侠
 \*/
public class IOClient {

 public static void main(String[] args) {
 new Thread(() -> {
 try {
 Socket socket = new Socket("127.0.0.1", 8000);
 while (true) {
 try {
 socket.getOutputStream().write((new Date() + ": hello world").getBytes());
 Thread.sleep(2000);
 } catch (Exception e) {
 }
 }
 } catch (IOException e) {
 }
 }).start();
 }
}
\`\`\`

\## NIO
NIO使用少量的线程去监听很多过个IO事件，监听到事件后，可以让其他线程去执行IO操作，也就是有专门负责监听事件的线程，那么并发量大的时候，这个线程不需要阻塞，可以一直轮训IO事件，来一个事件，后续的read等IO操作可以交给其他线程，而BIO中IO事件监听及IO操作均是由一个线程去完成，并且这个过程会阻塞，并发量大的时候只能新开启线程去处理。

![](1595909486204-46cd8cd1-5498-4e20-91f0-e33660df7b63.png)

![](1595909581379-f83a5d19-d9fc-4f86-b3f9-50a7ebbeb6d1.png)
\`\`\`java
/\\*\\*
 \\* @author 闪电侠
 \*/
public class NIOServer {
 public static void main(String[] args) throws IOException {
 Selector serverSelector = Selector.open();
 Selector clientSelector = Selector.open();

 new Thread(() -> {
 try {
 // 对应IO编程中服务端启动
 ServerSocketChannel listenerChannel = ServerSocketChannel.open();
 listenerChannel.socket().bind(new InetSocketAddress(8000));
 listenerChannel.configureBlocking(false);
 listenerChannel.register(serverSelector, SelectionKey.OP\_ACCEPT);

 while (true) {
 // 监测是否有新的连接，这里的1指的是阻塞的时间为 1ms
 if (serverSelector.select(1) > 0) {
 Set set = serverSelector.selectedKeys();
 Iterator keyIterator = set.iterator();

 while (keyIterator.hasNext()) {
 SelectionKey key = keyIterator.next();

 if (key.isAcceptable()) {
 try {
 // (1) 每来一个新连接，不需要创建一个线程，而是直接注册到clientSelector
 SocketChannel clientChannel = ((ServerSocketChannel) key.channel()).accept();
 clientChannel.configureBlocking(false);
 clientChannel.register(clientSelector, SelectionKey.OP\_READ);
 } finally {
 keyIterator.remove();
 }
 }

 }
 }
 }
 } catch (IOException ignored) {
 }

 }).start();

 new Thread(() -> {
 try {
 while (true) {
 // (2) 批量轮询是否有哪些连接有数据可读，这里的1指的是阻塞的时间为 1ms
 if (clientSelector.select(1) > 0) {
 Set set = clientSelector.selectedKeys();
 Iterator keyIterator = set.iterator();

 while (keyIterator.hasNext()) {
 SelectionKey key = keyIterator.next();

 if (key.isReadable()) {
 try {
 SocketChannel clientChannel = (SocketChannel) key.channel();
 ByteBuffer byteBuffer = ByteBuffer.allocate(1024);
 // (3) 面向 Buffer
 clientChannel.read(byteBuffer);
 byteBuffer.flip();
 System.out.println(Charset.defaultCharset().newDecoder().decode(byteBuffer)
 .toString());
 } finally {
 keyIterator.remove();
 key.interestOps(SelectionKey.OP\_READ);
 }
 }

 }
 }
 }
 } catch (IOException ignored) {
 }
 }).start();

 }
}
\`\`\`

\## netty
jdk提供的nio不好用所以有了netty

\`\`\`java
/\\*\\*
 \\* @author 闪电侠
 \*/
public class NettyServer {
 public static void main(String[] args) {
 ServerBootstrap serverBootstrap = new ServerBootstrap();

 NioEventLoopGroup boss = new NioEventLoopGroup();
 NioEventLoopGroup worker = new NioEventLoopGroup();
 serverBootstrap
 .group(boss, worker)
 .channel(NioServerSocketChannel.class)
 .childHandler(new ChannelInitializer() {
 protected void initChannel(NioSocketChannel ch) {
 ch.pipeline().addLast(new StringDecoder());
 ch.pipeline().addLast(new SimpleChannelInboundHandler() {
 @Override
 protected void channelRead0(ChannelHandlerContext ctx, String msg) {
 System.out.println(msg);
 }
 });
 }
 })
 .bind(8000);
 }
}

/\\*\\*
 \\* @author 闪电侠
 \*/
public class NettyClient {
 public static void main(String[] args) throws InterruptedException {
 Bootstrap bootstrap = new Bootstrap();
 NioEventLoopGroup group = new NioEventLoopGroup();

 bootstrap.group(group)
 .channel(NioSocketChannel.class)
 .handler(new ChannelInitializer() {
 @Override
 protected void initChannel(Channel ch) {
 ch.pipeline().addLast(new StringEncoder());
 }
 });

 Channel channel = bootstrap.connect("127.0.0.1", 8000).channel();

 while (true) {
 channel.writeAndFlush(new Date() + ": hello world!");
 Thread.sleep(2000);
 }
 }
}
\`\`\`

\#

\## 操作系统IO模型

阻塞：

windows IOCP

Linux epoll

max kqueue

非阻塞： 异步

linux aio

java linux 环境使用epoll

select vs poll vs epoll

[https://www.ulduzsoft.com/2014/01/select-poll-epoll-practical-difference-for-system-architects/](https://www.ulduzsoft.com/2014/01/select-poll-epoll-practical-difference-for-system-architects/)

阻塞 X 同步=理解问题

阻塞= 用户态指令不往下执行了 park了 wait了

一次调用是否立即返回= 异步

\## server模型

\### event Loop
![](1595919925544-b205d09d-23e6-4c8e-b94f-0333a20ceee1.png)

\### reactor pattern

![](https://cdn.nlark.com/yuque/0/2020/jpeg/290656/1595920156627-2ad0f037-4281-4c95-a353-794b477b4b3b.jpeg#align=left&display=inline&height=573&margin=%5Bobject%20Object%5D&originHeight=573&originWidth=1215&size=0&status=done&style=none&width=1215)

\### proactor
![](https://cdn.nlark.com/yuque/0/2020/jpeg/290656/1595920410564-a789d8d4-6e00-4ecb-b808-4391ab30b153.jpeg#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=960&size=0&status=done&style=none&width=960)

\# Bootstrap

\## 服务端启动
\*\*引导类ServerBootstrap \*\*

.group 设置线程组 ,线程组 is ExecutorService

.channel设置IO模型

attr & option 分为 父和child。

.attr 属性map配置

.childAttr

.option tcp参数配置

.childOption

.bind

\## 客户端启动
\*\*引导类Bootstrap \*\*

.connect

.bind 和.connect return ChannelFuture，

ChannelFuture extends j.u.c.current.

通过addListener 添加回调,可以在回调中控制重新绑定和重连（指数退避

1 通过pipeline()获取责任链，添加handler

2 handler集成内置\`\*\*ChannelInboundHandlerAdapter \*\*\`重新方法

3 读写都是通过ByteBuf对象操作

小知识点：

可以通过线程池的ScheduledExecutorService.schedule 方法延迟执行

\# ByteBuf

![image.png](1595927821516-866248d2-f954-4f27-ac92-e1de3c1bd35b.png)

byteBuf is 字节容器

写数据时扩容，capacity=>maxCapacity

\## 容量 API

\## 读写指针相关的 API

\## 读写 API
字节

writeBytes(byte[] src) 与 buffer.readBytes(byte[] dst)

\## 复制
slice()、duplicate()

不同指针，相同存储

copy()

两套存储

\## 回收
netty使用了堆外内存，不会被GC回收

通过引用计数方式回收

release() 与 retain()

\# 编解码

通信协议设计 定义规则

![image.png](1595929298295-0660edb7-5529-409e-85be-8a4a3ef6431e.png)

魔数的作用：

约定作用，便于server只处理和约定的通信包

java对象 -序列号> 二进制 byte[]->ByteBuf= 编码

ByteBuf->byte[] -反序列化> java对象 = 解码

\## duubo 报文协议

![](https://cdn.nlark.com/yuque/0/2020/jpeg/290656/1595929895941-f0238c03-4463-4062-92d4-215f6abaab0a.jpeg#align=left&display=inline&height=496&margin=%5Bobject%20Object%5D&originHeight=496&originWidth=735&size=0&status=done&style=none&width=735)

\## 工具类
ByteToMessageDecoder

MessageToByteEncoder

\# pipeline&channelHandler

\## 设计
一条连接对应着一个 Channel

ChannelPipeline is 双向链表 和Channel时一对一关系

ChannelPipeline 节点是\`ChannelHandlerContext\`  ，Context has handler

![image.png](1595931209027-1e169c1b-6182-4720-b825-02f8caa2b6c2.png)

\`ChannelInboundHandler\`  读处理 channelRead 数据从物理层上升到我们的应用层

\`ChannelOutBoundHandler\` 写处理 write 层层协议的封装，直到最底层的物理层

\`\`\`java
@Override
public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
 ctx.fireChannelRead(msg);
}
\`\`\`
第二个参数 msg 是上一个 handler的输出

\## SimpleChannelInboundHandler
通过泛型实现 packet和handler的绑定

\## 解决 if else 问题
将解码放在pileline前，编码放在pileline后，中间的一个packet一个handler ，直接操作对象

\## 半包，粘包
原因：tcp/ip底层是按照字节流来发送的和应用层是不对应的

处理办法：

半包，读直到能构成一个完整的包

粘包，读构成完整包的部分，剩下的仍保留在缓冲区中

\### 内置处理类

\#### 固定长度的拆包器 FixedLengthFrameDecoder

\#### 行拆包器 LineBasedFrameDecoder
换行符分割

\#### 分隔符拆包器 DelimiterBasedFrameDecoder
自定义换行符

\#### 基于长度域拆包器 LengthFieldBasedFrameDecoder
通过魔数拒绝非我协议在此类实现，通过继承

![image.png](1595946106126-238a9c80-bdfe-434a-9055-78e9ba162e9f.png)

7=4+1+1+1 偏移量

4=数据长度字段长度

\`new LengthFieldBasedFrameDecoder(Integer.MAX\_VALUE, 7, 4);\`

\# handler生命周期

handlerAdded() -> channelRegistered() -> channelActive() -> channelRead() -> channelReadComplete()

\`channelInactive() -> channelUnregistered() -> handlerRemoved()\`

注册到线程 从线程解绑

就绪 所有pipe handler都添加好

可读

handler支持热拔插，可以在建立连接后动态增删handler

\# ChannelGroup
方便对一组channel进行操作

\# 心跳
\*\*IdleStateHandler\*\*