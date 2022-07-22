\# pandor-hsf-spring-boot-autoconfigure
报错 Bean property 'interfaceClass' is not writable or has an invalid setter method.

![image.png](1598429866396-2a898494-dbae-43cb-a7f6-1533067cf4a9.png)

![image.png](1598429882509-751636c7-6fe9-4dca-bc36-2480b812f9f4.png)

错误：

Error setting property values; nested exception is org.springframework.beans.NotWritablePropertyException: Invalid property 'interfaceClass' of bean class [com.taobao.hsf.app.spring.util.HSFSpringConsumerBean]: Bean property 'interfaceClass' is not writable or has an invalid setter method.

新版的HSFSpringConsumerBean有了：

![image.png](1598429963061-0f5dbb07-2e75-45d6-b08f-2cbe421582ef.png)

解：

@RunWith(PandoraBootRunner.class)

@DelegateTo(SpringRunner.class)

使用Pandora容器会正确加载sar包中的类文件

\_