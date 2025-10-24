# 泛型
同其它高级强类型语言，Rust也支持泛型

## 声明
如实现加法运算
```rust
fn add<T: std::ops::Add<Output = T>>(a: T, b: T) -> T {
    a + b
}
```
rust 并不知道自定义类型如何进行加法运算
所以在使用加号时，要指明`T`必须实现`std::ops::Add` trait

这段代码还有另外的格式
```rust
fn add<T>(a: T, b: T)
    where T: std::ops::Add<Output = T>,
{
    a + b
}
```

> 这里的 `Output = T` 是`Add` trait的关联类型，表示返回值类型

