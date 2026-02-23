# rust

## 安装 Rust（Windows）

推荐使用 `rustup`，方便后续切换工具链和升级。

```powershell
winget install --id Rustlang.Rustup --source winget --accept-source-agreements --accept-package-agreements
```

## 验证安装

```powershell
rustup --version
rustc --version
cargo --version
```

如果命令找不到，先重开终端再试一次。

## 常用命令

### 更新工具链

```powershell
rustup update
```

### 查看已安装工具链

```powershell
rustup toolchain list
```

### 设置默认工具链

```powershell
rustup default stable
```

### 创建并运行第一个项目

```powershell
cargo new hello-rust
cd hello-rust
cargo run
```

## 经验总结

1. `winget` 安装 `Rustlang.Rustup` 后，`~\.cargo\bin` 会放置 `rustup/rustc/cargo`。
2. 用户级 `Path` 即使已经包含 `~\.cargo\bin`，当前终端会话也可能还不可见。
3. 最稳妥做法是重开终端；如果想每次启动都兜底，可在 PowerShell profile 中补一段：

```powershell
$cargoBin = Join-Path $HOME ".cargo\bin"
if ((Test-Path $cargoBin) -and -not (($env:Path -split ';') -contains $cargoBin)) {
    $env:Path = "$cargoBin;$env:Path"
}
```

4. 验收不要只看 `rustup`，至少同时确认 `rustc` 和 `cargo` 版本。
