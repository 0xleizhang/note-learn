\# 创建型

\## 单例 singleton
\`\`\`
public enum Singleton {
 INSTANCE;
 private T t = new T();//内部状态

 Singleton（）{
 t = new T();//初始化方法2
 }
 public T getInstance(){
 return t;
 };
}
\`\`\`

\## 工厂 Factory

\# 结构型

\## 代理
java动态代理
\`\`\`
public class Main {
 public static void main(String[] args) {
 InvocationHandler handler = new InvocationHandler() {
 @Override
 public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
 System.out.println(method);
 if (method.getName().equals("morning")) {
 System.out.println("Good morning, " + args[0]);
 }
 return null;
 }
 };
 Hello hello = (Hello) Proxy.newProxyInstance(
 Hello.class.getClassLoader(), // 传入ClassLoader
 new Class[] { Hello.class }, // 传入要实现的接口
 handler); // 传入处理调用方法的InvocationHandler
 hello.morning("Bob");
 }
}

interface Hello {
 void morning(String name);
}

\`\`\`

\## 组合
adapter适配，bridge桥接，装饰decorator,

外观facade:对外集成，封装外部接口复杂性到简单接口

代理proxy,组合composite

\# 行为型

\## 责任链 Chain of Responsibility