# 包和模块
我们这里拿一个计算器项目为示例，展示rust中包与模块间的组成关系。
此项目目录结构是这样的
```
/home/x0710/rustLearn/calculator/
├── calculator
│   ├── Cargo.toml
│   └── src
│       └── main.rs
├── Cargo.lock
├── Cargo.toml
└── math_utils
    ├── Cargo.toml
    └── src
        ├── base
        │   └── mod.rs
        ├── lib.rs
        └── normal.rs

6 directories, 8 files
```
## 工作空间(Workspace)
工作空间就是项目的根目录，这里所举的例子和使用`cargo new`的不同
工作空间里面可以有多个项目,需要在_Cargo.toml_中声明

```Cargo.toml
[workspace]
members = [
    "math_utils",
    "calculator"
]
```
这里的`members`表示工作空间中使用了哪些项目

## 项目(Package),又可以叫作_库_
rust中有两种库：
- 二进制库  可以通过cargo run运行
- 普通库    不可运行，作为工具供他人使用

一个项目由多个包共同组成，用来管理这些包的软件叫作_cargo_
在项目的_Cargo.toml_中存储了项目所使用的模块。

让我们来看下_calculator_的cargo配置
```calculator/Cargo.toml
[package]
name = "calculator"
version = "0.1.0"
edition = "2021"

[dependencies]
math_utils = { path = "../math_utils" }
```
> 注意：引入自己写的_crate 库_时，一定要用大括号括起，用`path`指明引用包位置
> 如果要引入版本，用逗号隔开，使用`version`进行指定。


## 什么是cargo？
> 全世界最好用的包管理工具！

cargo是rust的包管理工具，负责调用rustc编译工具，引入第三方包组件，调试、清理等功能。
和其它语言一样，rust同样具有包管理系统

正如同java有maven,gradle;C有CMake一样，rust的包管理工具为Cargo
而包又由不同的_模块_组成

## 模块(module)
一个包由若干功能共同拼凑出的，_module_就像是java中的类
但与之不同的是，在rust中，一个_module_下可以再嵌套多个_module_

模块间的关系如同unix中文件关系一样，它们有共同的_包根(crate root)_
由共同的_包根_用`::`的形式进行引入

### 定义
模块有两种实现方式，通过路径或文件
我们可以通过`mod`定义一个模块


#### 通过路径的方式定义
注意

### 使用



## 
## 包(crate)


###
1. Cargo.toml的dependencies中，如果引入自己写的包，就不需要引入version,要写路径 `path = "../math_utils"`
如果想再引入版本，需要使用大括号进行包围
