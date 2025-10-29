# 多线程
## `spawn()` 线程的生成
```rust
// 创建一个线程并立即调用
let handle = thread::spawn(|| {
    // doing sth...
});
```
> 注意：rust中进行spawn就立刻执行线程了

## `Mutex` 互斥锁
在rust多线程中，`std::sync::Arc`智能指针是很常用的
其用于在不同线程中共享一个对象

```rust
// 把数值0作为锁保护的实例
let lock = Arc::new(Mutex(0));

let c = Arc::clone(&lock); // 使lock在其它线程也可以访问
let handle = thread::spawn(move || { // 这里move表示把所有权移到线程
    /*
    这里使用了c，在main中的c的所有权已经移入新的线程中
    调用了lock表示获取锁

    如果其它线程正持有锁，会进行等待，如果线程中发生panic，则对其进行解包会发生panic
    */
    let mut val = c.lock().unwrap();
    *val += 1; // 数值自增1
});

handle.join().unwrap();

```

## `mpsc` 消息传递
> _Multiple Produce, Single Consume_
顾名思义，多个线程发消息，一个线程接消息
```rust
// channal(usize)可接参数，表示最大异步缓存
let (tx, rx) = mpsc::channal();

// 如果创建多个线程共用tx,需要tx.clone()
let tx_clone = tx.clone();
let handle = thread::spawn(move || {
    for i in 0..10 {
        // 如果rx已经关闭会引发panic
        tx_clone.send(i).unwrap();

        thread::sleep(Duration::from_millis(10));
    }
});

// 注意，这里需要释放tx，上面传递的是tx.clone()，如果存在tx则会一直监听接收
drop(tx);
loop {
    match tx.try_recv() {
        Ok(msg) => println!("Msg: {}", msg),
        Err(mpsc::TryRecvErr::Empty) => thread::sleep(Duration::from_millis(100)),
        Err(mpsc::TryRecvError::Disconnected) => break,
    }
}

```

## `Barrier` 屏障
进入状态的线程达到一定数量后，才开始执行
```rust
let barrier = Arc::new(Barrier::new(5));
let handles = Vec::with_capacity(5);

for i in 0..5 {
    let c = Arc::clone(&barrier);
    let handle = thread::spawn(move || {
        println!("spawn {i} ready!");
        c.wait(); // 注意这里不需要.unwrap();
        println!("spawn {i} running!");
    });
    handles.push(handle);
}
for spawn in handles {
    spawn.join().unwrap();
}

```


2025年 10月 29日 星期三 21:52:40 CST
