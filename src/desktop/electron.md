# electron

## 创建应用

```powershell
npx create-electron-app@latest my-app
cd my-app
npm start
```

Electron 由主进程创建窗口，渲染进程显示界面。启用 `contextIsolation`，关闭不必要的 `nodeIntegration`，只通过 preload 中定义的最小 IPC API 暴露受控能力。所有 IPC 入参都应校验。

## 最小窗口

```js
const { app, BrowserWindow } = require('electron')

app.whenReady().then(() => {
  const win = new BrowserWindow({
    width: 1000,
    height: 700,
    webPreferences: { contextIsolation: true, nodeIntegration: false },
  })
  win.loadURL('http://localhost:5173')
})
```

## 常用命令

```bash
npm start
npm run make
npm run publish
```

## 经验总结

1. 主进程负责窗口和系统能力，渲染进程只负责界面。
2. 不加载不可信网页；加载外部页面时必须重新审视权限配置。
3. 打包前在干净环境测试自动更新、文件权限和 Windows 签名。
