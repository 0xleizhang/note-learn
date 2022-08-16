**

[📎threads_report.txt](https://yuque.antfin.com/attachments/lark/0/2020/txt/314166/1595227630204-e8640183-fdfd-4379-b075-6dea2282cb41.txt)

通过thread dump分析看到发生了死锁

# 过程分析：
spring容器启动refresh过程中DefaultSingletonBeanRegistry.getSingleton 通过synchronized加了锁（图一 0x4989）

继续往下执行，AnnotationBean这个 BeanPostProcessor扫描需要dubbo处理的类，包括装配标有dubbo @ Reference注解的远程bean

顺着堆栈ReferenceConfig.get 往下看,发现future.get()调用阻塞了 (图二)。导致spring容器的singletonObjects对象锁一直无法释放。

当schedulerx的任务下发到工作线程后，工作线程会调用SpringContext.getBean创建一个Processor bean。最终也会调到DefaultSingletonBeanRegistry.getSingleton 需要获取singletonObjects对象锁 但是这个锁被main线程持有，因为main线程dubbo处理阻塞进而导致schedulerx processor无法创建

话说回来，其实如果dubbo将将future.get()换成带超时参数的get(long timeout, TimeUnit unit) 就不会阻塞主线程了。

# 推论：
如果主线程在装配bean过程中阻塞了，则schedulerx的任务就无法正常处理，还可能的场景包括装配bean需要访问数据库数据库不通导致阻塞。

为了理解以上过程简化模拟代码：

```java
public class Demo {
 private HashMap map = new HashMap();
 static Demo demo = new Demo();
 static ExecutorService executorService = Executors.newSingleThreadExecutor();

 public static void main(String[] args) {


 Thread t = new Thread(() -> {

 sleep(2000L);
 System.out.println("a开始工作");
// springContext.getBean 加锁
 synchronized (demo.map) {

 System.out.println("a 或获得所");
 }
 });
 t.setName("work Thread");
 t.start();

 Thread t3 = new Thread(() -> {

 sleep(3000L);
 System.out.println("t3 开始工作");
// springContext.getBean 加锁
 synchronized (demo.map) {

 System.out.println("t3 或获得所");
 }
 });
 t3.setName("work2 Thread");
 t3.start();

 // springContext.getBean 加锁
 synchronized (demo.map) {
 Future future = executorService.submit(new Callable() {
 @Override
 public Object call() throws Exception {
 // 模拟 dubbo 阻塞
 LockSupport.park();
 return "obj";
 }
 });
 System.out.println("b 阻塞");
 try {
 Object o = future.get();
 } catch (InterruptedException e) {
 e.printStackTrace();
 } catch (ExecutionException e) {
 e.printStackTrace();
 }

 }
 }

 static void sleep(long time) {
 try {
 Thread.sleep(time);
 } catch (InterruptedException e) {
 e.printStackTrace();
 }
 }
}
```

# 解决办法：
如果想做到无论主线程bean装配是否成功都不影响定时任务processor执行。

可以让processor类在SchedulerxWorker类装配之前就初始化装配好，这样当任务下发getBean的过程中就直接能从cache中取bean,不需要加锁了，如图5，图6

# 附件：


图一

![](1595483887946-c092945c-f32e-430f-bcf1-d46964975d5a.png)

图二

![](1595483888155-5e6244e0-f867-4aed-95de-ec7ed1a23f0f.png)

图三

![](1595483888575-5ab125fe-6e39-489b-a72b-3b8b4c3dfc2b.png)

图四

![](1595483889029-0bda5e8a-d40a-42b7-b1ee-79393c18c257.png)

图5

![](1595483889189-5ed05825-e9bc-454b-99e2-e05ad3780eee.png)

图6

![](1595483889554-d8b4ffa4-ba84-44fe-9f4f-8a4b27b3af7e.png)