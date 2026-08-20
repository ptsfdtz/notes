# tools

日常开发环境、命令行与网络工具的安装和使用记录。

- Windows 优先使用 `winget` 安装软件；安装后重新打开终端，使 PATH 生效。
- 涉及管理员权限的命令，请在管理员终端中执行。
- Linux 发行版的包管理器和服务管理方式不同，执行前先确认系统版本。

## 常用检查

```powershell
Get-Command git
Get-Command docker
$env:Path -split ';'
where.exe node
```

命令找不到时，优先确认是否安装成功、PATH 是否已更新，以及当前终端是否在安装前就已打开。
