约定大于配置

META-INF/spring.factories

```
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.demo.xxxAutoConfiguration
```

怎么找配置类

去扫描META-INF/spring.factories

找的过程就是SPI Service Provider Interface

服务发现机制，就类比开发过程中的接口对接



ServiceLoader.load(IxxxService.class)



<details><summary>click me</summary>
<p>
# 123
</p>
</details>


### 21323

````
​```
1231
​```
````

## Spring源码

> IOC、DI、AOP、MVC、循环依赖、多级缓存

Spring干了一件什么事呢？

new User() => container容器 => ConcurrentHashMap

读取配置文件

- 通过ClassPathXmlApplicationContext去加载xml配置文件
- 通过Configuration注解

解析配置文件

创建实例

使用

销毁

什么是实例化？

对象创建的过程

实例化完成的对象，可以直接进行使用吗？

初始化才是真正的赋值

赋值，执行初始化方法init