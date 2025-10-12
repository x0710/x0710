# `find` 查找命令
`find` 是 Linux/Unix 系统中 **强大的文件搜索工具**

** `find` 语句中，参数都是以**一个**`-`引出的，并非两个。

## 命令格式
`find [搜索路径] [搜索条件] [相关操作]`

## 食用方法
* 使用 `-a` 表示并且(AND)，用 `-o` 表示或者(OR),如果不加表示并且。

* 用括号 `\(...\)` 控制优先级（注意转义）
在find语句中，使用小括号需要转义(使用\\符号)

### ** 常用搜索条件**

| 条件          | 含义             | 示例                                  |
| ----------- | -------------- | ----------------------------------- |
| `-name`     | 按文件名匹配（区分大小写）  | `find . -name "*.txt"`              |
| `-iname`    | 按文件名匹配（不区分大小写） | `find . -iname "*.TXT"`             |
| `-type`     | 文件类型           | `f` 普通文件、`d` 目录、`l` 符号链接            |
| `-size`     | 文件大小           | `+100M` 大于 100MB、`-10k` 小于 10KB     |
| `-mtime`    | 修改时间           | `-mtime -7` 最近 7 天修改过               |
| `-user`     | 所有者            | `find . -user root`                 |
| `-group`    | 所属组            | `find . -group staff`               |
| `-perm`     | 权限             | `find . -perm 644`                  |
| `-regex`    | 正则匹配路径         | `find . -regex ".*\.\(rs\|toml\)$"` |
| `-maxdepth` | 最大搜索深度         | `find . -maxdepth 2 -name "*.rs"`   |
| `-mindepth` | 最小搜索深度         | `find . -mindepth 1 -name "*.md"`   |

> 一般以**time**结尾单位为天，以**min**结尾为分钟

> 注意：`-name` 匹配的是 **文件名**，而 `-regex` 匹配的是 **整个路径**
---

### ** 执行操作**

* `-exec` 可以对找到的每个文件执行命令

```bash
# 删除所有 .tmp 文件
find . -name "*.tmp" -exec rm {} \;

# 查看所有 .rs 文件的行数
find . -name "*.rs" -exec wc -l {} \;

# 使用 + 批量执行，提高效率
find . -name "*.rs" -exec wc -l {} +
```

* `{}` 会被替换为匹配的文件名
* `\;` 表示命令结束
* `+` 表示尽量批量处理（效率高）

---

## 举例
```bash
# 查找当前及子目录下以.rs或.toml结尾的文件
find . (-name "*.rs" -o -name "*.toml")

# 也可以写成
find . -regex '*.(rs|toml)$'

# 与第一个例子同理
find . \( -name "*.rs" -o -name "*.toml" \)
```

> 注意：`-name` 参数使用的是[_Glob_](glob.md)，并非是_正则表达式_。

> 注意：第二个示例中把双引号_"_换为了单引号_'_，这是为了防止[bash扩展](BashScript.md#bash扩展)

```bash
# 查找当前目录及子目录所有 .rs 或 .toml 文件，并打印内容
find . \( -name "*.rs" -o -name "*.toml" \) -exec cat {} +

# 查找最近 7 天修改过的 .md 文件
find . -name "*.md" -mtime -7

# 查找用户 act 的 home 下 move 目录里的所有 .txt 文件
find ~act/move -name "*.txt"
```

2025年 10月 12日 星期日 14:04:32 CST
