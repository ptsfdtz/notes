# gin

## 创建项目

```powershell
mkdir gin-demo
cd gin-demo
go mod init example.com/gin-demo
go get github.com/gin-gonic/gin
```

## 最小服务

```go
package main

import "github.com/gin-gonic/gin"

func main() {
    r := gin.Default()
    r.GET("/health", func(c *gin.Context) {
        c.JSON(200, gin.H{"status": "ok"})
    })
    r.Run(":8080")
}
```

运行 `go run .` 后访问 `http://localhost:8080/health`。生产环境应设置可信代理、校验输入、统一错误响应，并使用环境变量配置端口和数据库连接。

## 常用路由

```go
r.GET("/users/:id", func(c *gin.Context) {
    c.JSON(200, gin.H{"id": c.Param("id")})
})

r.POST("/users", func(c *gin.Context) {
    var input struct {
        Name string `json:"name" binding:"required"`
    }
    if err := c.ShouldBindJSON(&input); err != nil {
        c.JSON(400, gin.H{"error": err.Error()})
        return
    }
    c.JSON(201, input)
})
```

## 中间件

```go
r.Use(gin.Logger(), gin.Recovery())
```

`gin.Recovery()` 可以防止 panic 直接终止进程。认证、跨域、请求日志等逻辑也适合放在中间件中；不要在中间件里吞掉错误。

## 经验总结

1. 使用 `ShouldBindJSON` 校验输入，不要直接信任请求体。
2. 路由处理函数保持轻量，业务逻辑和数据访问放到独立包中。
3. 启动时通过环境变量读取 `GIN_MODE`、端口和连接串，生产环境设置 `GIN_MODE=release`。
