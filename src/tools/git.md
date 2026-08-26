# Git

## 一.安装 Git

1. 官网下载 [下载](https://git-scm.com/downloads)

2. Windows下载

```sh
winget install --id Git.Git -e --source winget
```

3. Linux 下载

```sh
sudo apt-get install git # Debian/Ubuntu
sudo yum install git     # CentOS/RHEL
```

## 二.配置 Git

在 powershell 中输入`git`检测是否配置完成

### 配置用户

1. 初始化 Git 仓库

```sh
git init
```

2. 设置用户名和邮箱

```sh
git config user.name '<your-name>'
git config user.email '<your-email>'
```

3. 查看邮箱用户配置

```sh
git config --list
```

4. 配置 git

进入 gitconfig 文件

```sh
code ~/.gitconfig # vscode
```

添加以下内容（`<your-name>`、`<your-email>` 替换为你自己的信息）

```sh
[user]
    name=<your-name>
    email=<your-email>
[http]
    proxy=http://127.0.0.1:7890 # 仅在使用代理时保留，按本机实际地址填写
[https]
    proxy=http://127.0.0.1:7890
[init]
    defaultBranch=main
[pull]
    ff=only
```

> 不使用代理时，直接删除 `[http]` / `[https]` 两段即可。

## 三.初次提交模板

1. 项目初始化

```sh
git init
echo "# README" > README.md
git add README.md
git commit -m "First commit"
```

2. 添加远程仓库链接

```sh
git remote add origin <仓库链接>
```

3. 默认分支 main

```sh
git branch -M main
```

4. 提交到 github 仓库

```sh
git push -u origin main
```

> 首次推送新分支用 `-u` 建立跟踪关系即可；`-f` 会强制覆盖远程历史，仅在你确认需要覆盖时使用。

## 四.常用命令

- 查看当前状态

```sh
git status
```

- 查看提交记录

```sh
git log
```

- 回退到上一个版本

```sh
git reset --hard HEAD^
```

- 回退到上上个版本

```sh
git reset --hard HEAD^^
```

- 回退到指定版本

```sh
git reset --hard <commit-id>
```

- 分支相关的操作

```sh
git branch ##查看分支

git branch <name> ##创建分支

git checkout <name> ##切换分支

git checkout -b <name> ##创建+切换分支

git merge <name> ##合并某分支到当前分支

git merge --no-ff -m "..." <name> ##使用普通模式合并分支，可以显示合并历史

git branch (-m | -M) <oldbranch> <newbranch> ##重命名分支

git branch -d <name> ##删除分支

git branch -D <name> ##强行删除未合并分支

git log --graph ##查看分支合并图

git log --graph --pretty=oneline --abbrev-commit ##也可以查看分支合并图

git tag <num> ##创建标签

git push --tags ##推送标签
```
