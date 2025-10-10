# 两数之和
## 题目
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

## 题解
```rust
// 就这么一段代码用了我3个小时去修正
use std::collections::HashMap;

impl Solution {
    pub fn two_sum(nums: Vec<i32>, target: i32) -> Vec<i32> {
        let mut map = HashMap::new();
        let mut retVal = Vec::with_capacity(2);

        for (i, vec_val) in nums.into_iter().enumerate() {
            let r = map.get(&vec_val);
            match r {
                Some(&val) => {
                    retVal.push(val);
                    retVal.push(i as i32);
                    break;
                },
                None => _ = map.insert(target-vec_val, i as i32),
            }
        }
        retVal
    }
}
```

## 笔记
1. 若想得到集合的迭代器，有如下方式
- into\_iter()   直接得到数据的所有权，会导致集合无法再次使用
- iter()        获得到数据的引用
- iter\_mut()    获得到数据的可变引用

2. 元组(truple)会通过模式匹配自动为引用数据进行解引用
```rust
// 这里因为调用了into_iter()，直接获得了所有权，不需要引用
for (i, val) in nums.into_iter().enumerate() {}

// 这里因为调用了iter()，得到的是&i32类型，通过使用模式匹配，使得val已经为i32类型
for (i, &val) in nums.iter().enumerate() {}
```

3. `if let` 语句
`if let` 适用于仅有**两种结果的类型**，多用于`Option::Some(\_)`以及`Result::Ok`
```rust
// 注意这里是单等于号
if let Some(&idx) = map.get(&vec_val) {
    // 因为调用`get()`是获取到值，在集合中数据并没有发生变化
    // 所以只获得了引用，故需要使用`&`进行接收
    ...
}else {
    ...
}
```
在某种程度上，`if let`语句可以使`match`语句更加简洁。

4. `_ =`
具有返回值的函数在调用后，若不接收返回值，需要显式声明，否则编译器会发出警告。
使用 `_ =` 接收返回值，以表明“我真的不需要返回值”。

> Wed Oct  8 03:54:34 PM CST 2025
