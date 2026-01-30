# Spring
* 什么是 Spring ？
Spring是指以SpringFramework为基础的SpringBoot, SpringMVC... 等产品的合集

* SpringFramework 和 SpringBoot 的区别在哪里？

SpringFramework 是


## 组件

### 一次请求的过程

** Servlet -> Service -> DAO -> 数据库 **
** 控制层 -> 业务层 -> 持久层 -> 数据库 **


## SpringIoC
负责组件的管理

### 接口

* `BeanFactory` 接口，是SpringIoC容器的标准接口
    * `ApplicationContext` 是`BeanFactory`的实现类，对原有进行扩展
        * `ClassPathXmlApplicationContext` 
        * `FileSystemXmlApplicationContext` 
        * `AnnotationConfigApplicationContext` 
        * `WebApplicationContext` 

### 配置方式

1. XML 配置文件
2. Java 注解
3. ** Java 配置类 **

#### XML 配置文件
在*resource*文件夹下面新建*.xml*文件，用`beans`标签包起来
相关`bean`属性：
| 元素 | 内容 |
| ---- | ---- |
| `id` | 组件的唯一标识符 |
| `class` | 组件对应的java类 |
| `factory-method` | 静态初始化方法名 |
| `facotry-bean` | 先通过这个bean得到实例，再通过实例去初始化另一个类 |


### IoC 核心功能: IoC / DI

1. IoC 控制反转
当对象控制权由应用程序转移到Spring管理

2. DI 依赖注入


