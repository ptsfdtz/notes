# python

## 安装 Python（Windows）

推荐使用 `winget` 安装官方版本：

```powershell
winget install --id Python.Python.3.14 --source winget --accept-source-agreements --accept-package-agreements --override "InstallAllUsers=0 PrependPath=1 Include_launcher=1 Include_pip=1"
```

说明：

1. `PrependPath=1` 会把 Python 和 Scripts 目录加入 `Path`。
2. `Include_launcher=1` 会安装 `py` 启动器。
3. `Include_pip=1` 会安装 `pip`。

## 验证安装

```powershell
python --version
pip --version
py --version
```

如果当前终端提示找不到命令，先重开终端再试。

## 虚拟环境

创建虚拟环境：

```powershell
python -m venv .venv
```

激活虚拟环境（PowerShell）：

```powershell
.\.venv\Scripts\Activate.ps1
```

退出虚拟环境：

```powershell
deactivate
```

## 常用命令

升级 `pip`：

```powershell
python -m pip install --upgrade pip
```

安装依赖：

```powershell
pip install <package-name>
```

导出依赖：

```powershell
pip freeze > requirements.txt
```

按依赖文件安装：

```powershell
pip install -r requirements.txt
```

## 经验总结

1. 本机实测通过 `winget` 安装后，`python.exe`、`pip.exe`、`py.exe` 都已安装在用户目录下：
   `C:\Users\<用户名>\AppData\Local\Programs\Python\Python314\`，即 `%LOCALAPPDATA%\Programs\Python\Python314\`。
2. 用户级 `Path` 虽然已更新，但当前已打开的终端会话不会自动刷新，重开终端后命令才会直接可用。
3. 如果执行 `python` 仍跳转到 Microsoft Store，需要在系统设置中关闭 App Execution Aliases 里的 `python.exe/python3.exe`。
4. 验收建议至少检查三项：`python --version`、`pip --version`、`py --version`。
