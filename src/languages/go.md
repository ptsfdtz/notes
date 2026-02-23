# go

## 安装 Go（Windows）

推荐优先使用 `winget` 安装：

```powershell
winget install --id GoLang.Go --source winget --accept-source-agreements --accept-package-agreements
```

也可以使用官方安装包：

- [Go 官方下载](https://go.dev/dl/)

## 验证安装

```powershell
go version
go env GOROOT
go env GOPATH
```

如果命令找不到，先重开终端再试一次。

## 模块和项目初始化

### 创建第一个项目

```powershell
mkdir hello-go
cd hello-go
go mod init hello-go
```

创建 `main.go`：

```go
package main

import "fmt"

func main() {
	fmt.Println("hello go")
}
```

运行项目：

```powershell
go run .
```

## 常用命令

```powershell
go mod tidy
go fmt ./...
go test ./...
go build ./...
```

## 常用配置

### 配置国内代理（可选）

```powershell
go env -w GOPROXY=https://goproxy.cn,direct
go env -w GOSUMDB=sum.golang.google.cn
```

查看当前配置：

```powershell
go env GOPROXY
go env GOSUMDB
```

恢复默认：

```powershell
go env -u GOPROXY
go env -u GOSUMDB
```

## 经验总结

1. `go install <module>@latest` 安装的可执行文件默认在 `GOPATH\bin`。
2. 如果安装了工具但命令不可用，先确认 `GOPATH\bin` 是否在 `Path` 中。
3. `go mod tidy` 建议作为日常命令，能及时清理和补齐依赖。
4. `go test ./...` 可以快速覆盖整个项目包的基础回归。
