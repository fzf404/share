## Gin框架入门

> [Github地址](https://github.com/gin-gonic/gin)
>
> [中文文档](https://www.topgoer.com/gin%E6%A1%86%E6%9E%B6/)

### 安装

```bash
# 1. 创建文件夹
mkdir go-web
# 2. 初始化项目
cd go-web
go mod init go-web
# 3. 安装
go get -u github.com/gin-gonic/gin
# 4. 运行
go run main.g
```

### HelloWorld

```go
package main

import (
	"net/http"

	"github.com/gin-gonic/gin"
)

func main() {
	// 1. 创建路由
	r := gin.Default()
	// 2. 绑定路由规则，执行的函数
	r.GET("/", func(c *gin.Context) {
		// 返回字符串, http 状态码 200
		c.String(200, "Hello World!")
	})

	r.GET("/ping", func(c *gin.Context) {
		// 返回JSON, http 状态码 200
		c.JSON(http.StatusOK, gin.H{
			"message": "pong",
		})
	})

	// 3. 监听 8080 端口
	r.Run(":8000")
}

```



