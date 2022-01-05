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
go run main.go
# 5. 接口测试工具
postman
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

### 参数获取方式

> 获取前端传来的数据

```go
// GET - http://0.0.0.0:8080/user?name=fzf404&password=123456
c.DefaultQuery("name","noname")
c.Query("password")

// POST - http://0.0.0.0:8080/user
c.DefaultPostForm("name", "noname")
c.PostForm("password")
```

## Gorm入门

> [Github地址](https://github.com/go-gorm/gorm)
>
> [中文文档](https://www.kancloud.cn/sliver_horn/gorm/content)

### 安装

```go
// 1. 安装
go get -u gorm.io/gorm
go get -u gorm.io/driver/mysql
```

## HelloWorld

```go
package main

import (
	"fmt"
	"strconv"

	"github.com/gin-gonic/gin"
	"gorm.io/driver/mysql"
	"gorm.io/gorm"
)

// 用户结构体
type User struct {
	ID       uint
	Name     string
	Age      int
	Password string
}

func main() {
	// 连接数据库
	// 用户名:密码@tcp(ip:port)/库名
	dsn := "root:1234@tcp(127.0.0.1:3306)/userinfo"
	db, err := gorm.Open(mysql.Open(dsn), &gorm.Config{})
	if err != nil {
		fmt.Println("mysql 连接失败: ", err)
	}

	r := gin.Default()

	r.GET("/login", func(c *gin.Context) {
		// 获取前端传来的参数
		username := c.Query("username")
		password := c.Query("password")
		// 空结构体实例
		var user User
		// 通过用户名查询实例
		db.Where("Name = ?", username).First(&user)
		// 验证密码和用户是否存在
		if user.ID != 0 && user.Password == password {
			// 登陆成功
			c.JSON(200, gin.H{
				"code": 1,
				"data": gin.H{
					"id":  user.ID,
					"age": user.Age,
				},
				"msg": "登录成功",
			})
			return
		}

		// 登陆失败
		c.JSON(200, gin.H{
			"code": 0,
			"data": nil,
			"msg":  "登录失败",
		})
	})

	r.POST("/regist", func(c *gin.Context) {
		// 获取前端传来的参数
		username := c.PostForm("username")
		password := c.PostForm("password")
		ageRaw := c.DefaultPostForm("age", "0")
		// 数据类型转换
		age, _ := strconv.Atoi(ageRaw)
		// 结构体实例
		user := User{
			Name:     username,
			Age:      age,
			Password: password,
		}
		// 写入数据库
		// 会写入userinfo 库 users 表
		result := db.Create(&user)
		
		if result.Error != nil  {
			c.JSON(200, gin.H{
				"code": 0,
				"data": nil,
				"msg":  "注册失败",
			})
			return
		}
		// 成功
		c.JSON(200, gin.H{
			"code": 200,
			"data": gin.H{
				"id":       user.ID,
				"username": user.Name,
			},
			"msg": "注册成功",
		})
	})
	r.Run()
}

```

