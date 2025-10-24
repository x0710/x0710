# `findmnt` 用于查看挂载点与设备之间的关系

可直接使用`findmnt /`查看根目录挂载位置
```bash
findmnt /
TARGET SOURCE    FSTYPE OPTIONS
/      /dev/sda1 ext4   rw,relatime
```
以下命令
`findmnt -no SOURCE /boot`
选项
`-n`表示不打印标题(no headings)
`-o` SOURCE 表示只输出“挂载源”


2025年 10月 13日 星期一 08:32:59 CST
