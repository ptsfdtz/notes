# Powershell

## 一.开启 powershell

1. `win + R` 输入 `powershell`

2. 管理员身份运行 `Ctrl + Shift + Enter`

## PowerShell 升级和 Windows Terminal 配置

1. 查看 PowerShell 当前版本

```powershell
$PSVersionTable
```

2. 更新 PowerShell

添加中科大镜像源
```powershell
winget source add --name winget --arg https://mirrors.ustc.edu.cn/winget-source
```

```powershell
winget search PowerShell # 查询可用的 PowerShell 包
```

3. 安装（微软发布的 PowerShell）

```powershell
winget install --id Microsoft.PowerShell -e
```

4. 打开 Windows Terminal 的 settings.json 并修改配置（示例，替换为你的 GUID）

```json
{
  "defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
  "profiles": {
    "list": [
      {
        "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
        "name": "PowerShell",
        "source": "Windows.Terminal.PowershellCore",
        "hidden": false
      }
    ]
  }
}
```

## 二. 文件相关命令

1. 进入文件夹

```powershell
cd .\
```

2. 返回上级目录

```powershell
cd ..
```

3. 创建目录 / 文件

```powershell
mkdir .\NewFolder

ni .\file.txt -ItemType File
```

4. 删除文件或目录

```powershell
rm .\file.txt
```

5. 移动 / 重命名

```powershell
mv .\source.txt .\dest.txt
```

6. 使用 VS Code 打开当前目录

```powershell
code .
```

7. 清空回收站（无提示）

```powershell
Clear-RecycleBin -Force -Confirm:$false
```

## 三. 常用命令

### 环境变量

1. 显示环境变量

```powershell
gci env:
```

2. 设置（追加）环境变量路径

```powershell
$env:Path += ";C:\你的\路径"
```

### 网络配置

1. 显示本机 IP

```powershell
ipconfig
```

2. 测试网络连通性

```powershell
ping <IP 或 主机名>
```

3. 关闭防火墙（谨慎）

```powershell
netsh advfirewall set allprofiles state off
```

4. 显示网络统计信息

```powershell
netstat -an
```

5. 显示本地路由表

```powershell
route print
```

6. 显示/查询防火墙规则

```powershell
Get-NetFirewallRule
```
