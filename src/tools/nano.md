# nano

## 一. linux安装 

```sh
sudo apt update && sudo apt install nano -y # Debian/Ubuntu系统
sudo yum install nano -y                     # CentOS/RHEL系统
sudo dnf install nano -y                     # Fedora系统
```

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