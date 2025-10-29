# `shuf` 随机生成
```bash
shuf testfile   # 将testfile文件中的内容按行打印并输出
```

```bash
shuf testfile -o outfile   # 将testfile文件中的内容按行打印并输出到outfile中
```

```bash
shuf -n 2 testfile   # 将testfile文件中的内容按行进行随机输出2条
```

```bash
shuf -n 1 -e e1 e2 e3   # 在-e选项后面的内容随机挑选1个元素
```

```bash
shuf -i 1-10    # 使用-i选项以指定范围  打乱1-10
```


2025年 10月 28日 星期二 10:16:52 CST
