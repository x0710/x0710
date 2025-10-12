#### Stow
一款GNU开源工具，最初用来管理源代码，后来逐渐演化为管理dotfiles的专门工具，
配合git食用性会更好。

### 用法
这里还是推荐在`$HOME`下面新建一个`dotfiles`文件夹，用来专门存放各种dotfile的地方
标准dotfiles文件文件夹应该是这样的
tree -da .
.
├── .git
│   ├── hooks
│   ├── info
│   ├── logs
│   │   └── refs
│   │       ├── heads
│   │       └── remotes
│   │           └── origin
│   ├── objects
│   │   ├── 27
│   │   ├── 34
│   │   ├── 96
│   │   ├── info
│   │   └── pack
│   └── refs
│       ├── heads
│       ├── remotes
│       │   └── origin
│       └── tags
├── hyprland
├── i3
│   └── .config
│       └── i3
├── nvim
│   └── .config
│       └── nvim
├── sway
│   └── .config
│       └── sway
├── vim
└── waybar
    └── .config
        └── waybar

34 directories

如此存放后，就可以使用下面的命令来创建目标程序的配置文件。
``` bash
stow -t $HOME nvim          #如果dotfiles在$HOME下，-t $HOME可以省略
```


