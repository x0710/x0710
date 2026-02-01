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
    * `ApplicationContext` 是`BeanFactory`的实现，对原有进行扩展
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
| `scope` | 可选值为`singleton`单例模式、`prototype`多例模式 |


### IoC 核心功能: IoC / DI

1. IoC 控制反转
当对象控制权由应用程序转移到Spring管理

2. DI 依赖注入
采用`property`标签，并通过`name`属性来指定Setter方法，value/ref属性来指定被设置的值


### ApplicationContext 的使用
使用以下代码获取在*.xml*中声明的IoC对象，
```java
ApplicationContext ctx = new ApplicationContext("*.xml");
// 方法1
BeanName bn1 = ctx.getBean("beanName");
// 方法2
BeanName bn2 = ctx.getBean("beanName", BeanName.class);
// 方法3，这只适用于只有一个对象时
BeanName bn3 = ctx.getBean(BeanName.class);

// 在IoC中，如果不特别声明，均使用单例模式
System.out.println(bn1 == bn2); // true
System.out.println(bn3 == bn2); // true
```

使用以下代码引入*.properties*文件
```xml
<context:property-placeholder location="classpath:<文件名>" />
```

#### 工厂方法
如果要使用工厂方法创建对象，可以在配置文件中指定`factory-method`，否则将调用无参构造器

相对于指定`factory-method`参数，更推荐为其实现一个正式的工厂类，并为其实现`FactoryBean<T>`接口
这样无需指定参数，IoC会自动识别工厂方法。
> 注意：此时指定的`id`不再指向工厂类，如果要指向工厂类，需要在其`id`前加上`&`表示工厂类

## `druid` 包
由阿里开发，管理数据库链接，不用于SQL语句的执行

食用方法：
```java
// 用于
DruidDataSource ds = new DruidDataSource();
// ds.set...这里用于配置sql的信息
// 配置好的DruidDataSource通常用于JdbcTemplate模板

// 用于SQL语句的执行
JdbcTemplate jt = new JdbcTemplate();
jt.setDataSouce(ds);
```

