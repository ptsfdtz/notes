# wails

## 安装wails

> 需要安装go 1.18+

[wails 官方安装文档](https://wails.io/docs/gettingstarted/installation)

```sh
go install github.com/wailsapp/wails/v2/cmd/wails@latest
```

## 创建项目

```sh
wails init -n my-wails-app -t vanilla
cd my-wails-app
wails dev
```

`wails dev` 会启动前端开发服务器和 Go 后端。首次运行时间较长时，先确认 Go、Node.js 和前端包管理器已正确安装。

## 前后端调用

在 Go 结构体中定义导出方法：

```go
type App struct{}

func (a *App) Greet(name string) string {
    return "Hello " + name
}
```

Wails 会生成前端绑定；前端通过生成的方法调用 Go 代码。

## 常用命令

```sh
wails doctor
wails dev
wails build
```

## 经验总结

1. 构建前运行 `wails doctor`，优先修复环境检查中的问题。
2. 不要把敏感配置直接编译进前端资源，配置应由 Go 端读取。
3. 生成的 bindings 不要手动修改，需要更新时重新生成。
