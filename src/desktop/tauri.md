# tauri

Tauri 使用系统 WebView 渲染前端，并由 Rust 提供原生能力。

```powershell
npm create tauri-app@latest
cd <项目名>
npm install
npm run tauri dev
```

在 `tauri.conf.json` 中只授权实际需要的能力。Rust command 的参数应使用强类型结构并校验，避免把任意文件路径或 shell 命令直接交给前端。

## 调用 Rust command

```rust
#[tauri::command]
fn greet(name: &str) -> String {
    format!("Hello, {name}!")
}
```

前端调用：

```ts
import { invoke } from '@tauri-apps/api/core'
const message = await invoke<string>('greet', { name: 'world' })
```

## 常用命令

```bash
npm run tauri dev
npm run tauri build
```

## 经验总结

1. `tauri build` 前确认已安装 Rust、Node.js 以及系统 WebView 依赖。
2. command 只暴露必要操作，文件读写等能力由 Rust 端限制允许目录。
3. 打包前在目标系统验证安装程序和签名，避免只在开发机运行。
