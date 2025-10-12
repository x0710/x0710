# Bash

## bash拓展
Bash 拓展（Bash Expansion）是 Bash shell 在解析命令行时自动替你生成、替换或修改字符串的功能。

> 注意：bash 会将双引号`"`内的内容进行bash拓展， 但在单引号中不会。

Bash 拓展主要包括以下几类：

1. [**文件名扩展（Globbing）**](#文件名扩展（Globbing）)
2. [**花括号扩展（Brace Expansion）**](#花括号扩展（Brace Expansion）)
3. [**算术扩展（Arithmetic Expansion）**](#算术扩展（Arithmetic Expansion）)
4. [**命令替换（Command Substitution）**](#命令替换（Command Substitution）)
5. [**变量扩展（Parameter Expansion）**](#变量扩展（Parameter Expansion）)
6. [**波浪线扩展（Tilde Expansion）**](#波浪线扩展（Tilde Expansion）)
7. [**路径名扩展（Pathname Expansion）**](#路径名扩展（Pathname Expansion）)

### **文件名扩展（Globbing）**
* 使用通配符匹配文件或目录
* 常用符号：

| 符号       | 含义                              |
| -------- | ------------------------------- |
| `*`      | 匹配任意长度的任意字符（包括零个字符）             |
| `?`      | 匹配单个字符                          |
| `[abc]`  | 匹配括号内任意一个字符                     |
| `[!abc]` | 匹配不在括号内的任意字符                    |
| `**`     | 递归匹配任意目录（需 `shopt -s globstar`） |

**示例：**

```bash
ls *.rs          # 匹配当前目录所有 .rs 文件
ls file?.txt     # 匹配 file1.txt、fileA.txt，但不匹配 file10.txt
ls **/*.rs       # 匹配当前目录及子目录所有 .rs 文件（递归）
```

---

### ** 花括号扩展（Brace Expansion）**

* 用 `{}` 生成多个字符串，常用于批量命令
* **不依赖实际文件存在**

**示例：**

```bash
echo file{1,2,3}.txt
# 输出: file1.txt file2.txt file3.txt

mkdir project/{src,bin,docs}
# 创建 project/src、project/bin、project/docs 三个目录
```

* 也可以用范围：

```bash
echo file{1..5}.txt
# 输出: file1.txt file2.txt file3.txt file4.txt file5.txt
```

---

### ** 算术扩展（Arithmetic Expansion）**

* 使用 `$(( expression ))` 进行整数运算
* 支持 `+ - * / %` 等运算符

**示例：**

```bash
a=5
b=3
echo $((a + b))  # 输出 8
echo $((a*b))     # 输出 15
```

* 可与变量组合：

```bash
i=1
echo $((i++))     # 输出 1，然后 i=2
```

---

### ** 命令替换（Command Substitution）**

* 使用 `$(command)` 或 `` `command` `` 获取命令输出作为值

**示例：**

```bash
files=$(ls *.rs)
echo $files
```

* 等价于：

```bash
echo `ls *.rs`
```

* 推荐用 `$(...)`，可读性更高，支持嵌套

---

### ** 变量/参数扩展（Parameter Expansion）**

* 通过 `${VAR}` 或 `${VAR:offset:length}` 操作变量
* 常用功能：

| 写法                | 功能              |
| ----------------- | --------------- |
| `${VAR}`          | 获取变量值           |
| `${VAR:-default}` | 变量为空或未定义时使用默认值  |
| `${VAR:=default}` | 变量为空或未定义时赋值为默认值 |
| `${VAR#pattern}`  | 去掉开头匹配模式        |
| `${VAR##pattern}` | 去掉最长开头匹配模式      |
| `${VAR%pattern}`  | 去掉结尾匹配模式        |
| `${VAR%%pattern}` | 去掉最长结尾匹配模式      |

**示例：**

```bash
file="project/main.rs"
echo ${file%.rs}  # 输出: project/main
echo ${file##*/}  # 输出: main.rs
```

---

### ** 波浪线扩展（Tilde Expansion）**

* `~` 表示用户主目录
* 可用 `~user` 指定其他用户的主目录

```bash
cd ~            # 当前用户主目录
ls ~/Documents  # Documents 文件夹
```

---

### ** 路径名扩展（Pathname Expansion）**

* Bash 在解析命令时，会根据文件系统展开路径名
* 与 Globbing 有关，但更底层
* 示例：

```bash
echo /usr/bin/*bash
# 输出 /usr/bin/bash /usr/bin/rbash 等匹配的文件
```

---

2025年 10月 12日 星期日 13:05:47 CST
