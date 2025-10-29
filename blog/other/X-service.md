# X 窗口系统
## 使用`xset`对X服务器进行配置
- `q` 表示查询当前配置情况
```bash
xset q  # 查询当前X服务器配置情况
xset s 1200 600 # 表示在1200s后启用屏保，以600s为一周期

xset dpms 60 360 3600 # 表示在60s后关闭屏幕，360s后断电屏幕，3600s后进入睡眠
```

# xss-lock
这个命令会在**进入屏保**、**关闭屏幕**时执行相应操作。
如果没有指定命令，默认行为是关闭屏幕
```bash
# 在进入屏保时执行bashfile.sh
xss-lock --transfer-sleep-lock -- <bashfile.sh>
```

# dpms
dpms为X服务器的电源管理系统



2025年 10月 28日 星期二 13:22:48 CST
