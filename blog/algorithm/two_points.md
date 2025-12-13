# 扩展双指针固定写法
```rust
let s = next().as_bytes();

let Some(mut l) = s.iter().position(|&x| x == b'a') else {
    println!("NO");
    continue;
};

let mut r = l;
let mut ok = true;

for c in b'b'..=b'z' {
    // 左右扩展：优先左有就左，否则用右
    if l > 0 && s[l - 1] == c {
        l -= 1;
    } else if r + 1 < s.len() && s[r + 1] == c {
        r += 1;
    } else {
        ok = false;
        break;
    }
}

println!("{}", if ok { "YES" } else { "NO" });

```


Thu Dec 11 09:05:27 PM CST 2025
