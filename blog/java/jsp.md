# MVC 架构
- module
- view      用户视图
- control   代码交互

---
# jsp(JavaServer Pages)
在tomcat中，JSP 会被编译为一个java文件，并在第一次访问目标jsp时对其动态加载(可选)
jsp中可以包含html语句和java语句

jsp主要负责[MVC架构](#MVC 架构)的_view_部分，在里面不适合加入过多逻辑处理语句

## jsp 指令
用来设置jsp页面的相关属性
- `<% %>`插入java语句
- `<%! %>`插入声明语句，声明的语句仅在加载时执行，长期有效
- `<%= %?`插入一个值
- `<%@ %>`对当前jsp页面进行配置，常见如下
    - `<%@ page language="java" contentType="text/html;charset=UTF-8" pageEncoding="UTF-8"%>`
    - `<%@ include "原封不动要插入文件的位置" %>
    - `<%@ taglib ... %>    引入标签库，可自定义标签

## jsp 隐含对象
事实上，在jsp页面中存在9种自动定义的隐含对象
对象名|说明
:------: |:----
out|`JspWriter`用来向客户端输出超文本
request|`HttpServletRequest`代表HTTP请求对象
response|`HttpServletResponse`代表HTTP响应对象
session|`HttpSession`代表用户会话对象
application|`ServletContext`代表Web应用程序上下文
config|`ServletConfig`包含有关当前jsp页面的配置信息
pageContext|`PageContext`的实例
page|`this`关键字，代表当前jsp实例
exception|`exception`

## jsp 行为
### 🧩 JSP 内置行为与对应 Java 语句对照表

| JSP 动作（Action）                                                               | 功能描述                                                | 等价 Java 语句 / Servlet 操作                                                                                                            |
| ---------------------------------------------------------------------------- | --------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `<jsp:useBean id="obj" class="com.demo.User" scope="session"/>`              | 查找或创建一个 JavaBean 实例                                 | `java Object obj = session.getAttribute("obj"); if (obj == null) { obj = new com.demo.User(); session.setAttribute("obj", obj); }` |
| `<jsp:setProperty name="obj" property="username" value="Tom"/>`              | 设置 JavaBean 属性                                      | `obj.setUsername("Tom");`                                                                                                          |
| `<jsp:getProperty name="obj" property="username"/>`                          | 读取 JavaBean 属性并输出                                   | `out.print(obj.getUsername());`                                                                                                    |
| `<jsp:include page="header.jsp"/>`                                           | 在运行时包含另一个 JSP/HTML 文件（内容会被执行）                       | `request.getRequestDispatcher("header.jsp").include(request, response);`                                                           |
| `<jsp:forward page="next.jsp"/>`                                             | 将请求转发到另一个 JSP/Servlet                               | `request.getRequestDispatcher("next.jsp").forward(request, response);`                                                             |
| `<jsp:param name="x" value="1"/>`                                            | 搭配 `<jsp:include>` 或 `<jsp:forward>` 向下个页面传参数       | `request.setAttribute("x", "1");`                                                                                                  |
| `<jsp:plugin type="applet" code="MyApplet.class" width="300" height="200"/>` | 生成用于加载 Java Applet 的 HTML `<object>` 或 `<embed>` 标签 | 输出相应的 HTML 插入代码                                                                                                                    |
| `<jsp:element name="tagName">...</jsp:element>`                              | 动态生成 XML/HTML 元素                                    | 输出 `<tagName>...</tagName>`                                                                                                        |
| `<jsp:attribute name="attr">...</jsp:attribute>`                             | 动态设置标签属性（通常与自定义标签结合）                                | 转换为 `setAttribute()` 调用或标签属性注入                                                                                                     |
| `<jsp:body>...</jsp:body>`                                                   | 定义标签体内容                                             | 转为标签体的 `doTag()` 内容                                                                                                                |
| `<jsp:text>...</jsp:text>`                                                   | 在 JSP 中强制输出纯文本（不会被解析）                               | 直接输出 `"..."` 到响应流                                                                                                                  |

### JavaBean
_JavaBean_ 是指符合_JavaBean 标准_的_java class_，参加以下资料
~~- 什么是[JavaBean](https://liaoxuefeng.com/books/java/oop/core/javabean/index.html)~~
- JspActions中的[JavaBean 食用方法](https://www.runoob.com/jsp/jsp-javabean.html)


## 注释
jsp有几种注释，如下：
```jsp
<%--
这种注释在浏览器访问时看不到注释中的内容
--%>
<!--
这种注释可以在浏览器中看到注释内容
-->
```

## EL 表达式


## 销毁操作
在jsp中插入`%! public void _jspDestroy() {} %`以重写销毁代码

常见的还有
```jsp
<%!
    // 初始化代码
    public void _jspInit() {}
    // 销毁代码
    public void _jspDestroy() {}
%>
```
> 注意：一些教程中所说的方法前没有_\__，没有下划线开始的方法在旧tomcat中可以不生效！


2025年 11月 02日 星期日 20:47:14 CST
