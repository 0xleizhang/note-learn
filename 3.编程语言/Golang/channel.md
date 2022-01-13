[官方文档](https://golang.google.cn/ref/spec#Channel\_types)

\# 语法
操作符合只有 <\- 决定读还是写取决于 ch 变量在左还是在右

c <- x 在左 ⬅️写入 大概意思是 c. value from x

在右 读取 x <- c 大概意思 x = get value from c

\*\*助记： 与=号类似，被修改的复制变量在左\*\*

c := make(chan bool) //创建一个无缓冲的bool型Channel

c <- x //向一个Channel发送一个值

<\- c //从一个Channel中接收一个值

x = <- c //从Channel c接收一个值并将其存储到x中

x, ok = <- c //从Channel接收一个值， ok标记是否已被close

\## 关于容量
make(chan int)

make(chan int, 0)

make(chan int,100)

如果没有设置容量，或者容量设置为0, 说明Channel没有缓存，只有sender和receiver都准备好了后它们的通讯(communication)才会发生(Blocking)。如果设置了缓存，就有可能不发生阻塞， 只有buffer满了后 send才会阻塞， 而只有缓存空了后receive才会阻塞。一个nil channel不会通信

​

​

​

\## close

往一个已经被close的channel中继续发送数据会导致run-time panic。

 After calling close, and after any previously sent values have been received, receive operations will return the zero value for the channel's type without blocking.

close ch之后原receive 操作非阻塞取出nil值，ok标记是否close

\## 关于读写方向
​

 Done() chan <- struct{} 写

 Done() <-chan struct{} 只读

编译器检查，避免channel滥用 代码整洁