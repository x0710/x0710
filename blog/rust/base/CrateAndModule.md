# 包和模块
我们这里拿一个计算器项目为示例，展示rust中包与模块间的组成关系。

## 项目(Package)
一个项目由多个包共同组成，用来管理这些包的软件叫作_cargo_

## 什么是cargo？
> 全世界最好用的包管理工具！
cargo是rust的包管理工具，负责调用rustc编译工具，引入第三方包组件，调试、清理等功能。
和其它语言一样，rust同样具有包管理系统
正如同java有maven,gradle;C有CMake一样，rust的包管理工具为Cargo

而包又由不同的_模块_组成
## 模块(module)
一个包由若干功能共同拼凑出的，_module_就像是java中的类
但与之不同的是，在rust中，一个_module_下可以再嵌套多个_module_
### 定义
在


## 
## 包(crate)
## 工作空间(Workspace)


###
1. Cargo.toml的dependencies中，如果引入自己写的包，就不需要引入version,要写路径 `path = "../math_utils"`
如果想再引入版本，需要使用大括号进行包围
