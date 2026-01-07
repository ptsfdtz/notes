# nano

## 一. linux安装 

| 说明 | 命令 |
| ---- | ---- |
| Ubuntu/Debian 系统安装 nano | `sudo apt-get install nano` |
| CentOS/RHEL 系统安装 nano | `sudo yum install nano` |
| Fedora 系统安装 nano | `sudo dnf install nano` |

## 二. Windows安装

```sh
winget install --id Nano.Nano -e --source winget
```

## 三. 配置

```sh
nano ~/.nanorc
```

添加以下内容

```sh
set linenumbers
set mouse
set autoindent
set softwrap
include "/usr/share/nano/*.nanorc"
```

## 四. 使用

```sh
nano 文件名

# 保存文件: Ctrl + O

# 退出 nano: Ctrl + X

# 查找文本: Ctrl + W

# 剪切文本: Ctrl + K

# 粘贴文本: Ctrl + U

# 撤销操作: Alt + U

# 重做操作: Alt + E
```