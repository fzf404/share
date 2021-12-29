> 踏入Golang的大门
>
> [教案](https://tour.go-zh.org/welcome/1)

## 环境安装

1. 安装vscode
2. 安装go1.16
3. vscode安装golang插件
4. 安装完成后验证

```bash
# 查看go版本
go version

# 换源
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct

# 新建文件
mkdir go-learn
cd go-learn

# 初始化go项目
go mod init learn-go

# 新建main.go
package main

import "fmt"

func main() {
	fmt.Println("Hello, 世界")
}

# 运行
go run main.go
```

## VsCode插件

```bash
# 安装失败则执行以下命令

# 换源
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct

# a
go get -v github.com/uudashr/gopkgs/v2/cmd/gopkgs
go get -v github.com/ramya-rao-a/go-outline
go get -v github.com/cweill/gotests/gotests
go get -v github.com/fatih/gomodifytags
go get -v github.com/josharian/impl
go get -v github.com/haya14busa/goplay/cmd/goplay
go get -v github.com/go-delve/delve/cmd/dlv
go get -v honnef.co/go/tools/cmd/staticcheck
go get -v golang.org/x/tools/gopls
```



## 基础语法

### 依赖库

> 使用 import 引入依赖库

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	fmt.Println("The time is", time.Now())
}
```

## 函数

```go
package main

import "fmt"

// 函数名(传入变量名 变量类型) 传出变量类型 { }
func addsub(x, y int) (int, int) {
	return x + y, x - y
}

func main() {
  // 调用函数
	fmt.Println(addsub(42, 13))
}

// 55 29
```

## 变量

```go
package main

import "fmt"

// 全局变量 变量类型
var c bool
var python string = "Good"

func main() {
  // 变量赋值
  c = true
  
  // 自动数据类型
  java := "No"
  golang := 666
  
  // 不换行打印
  fmt.Print(c)
  // 换行打印
  fmt.Println(python, java)
  // 格式化打印
  fmt.Printf("Go: %v", golang)
}

/* 输出:
trueGood No
Go: 666
*/
```

## for

```go
package main

import "fmt"

func main() {
	sum := 0
  
  // 初始化 判断 一次循环后执行
	for i := 0; i < 10; i++ {
		sum += i
	}
	fmt.Println(sum)
  
  // 无限循环
  for {
	}
  
}
```

## if

```go
import (
	"fmt"
	"math"
)

// 函数名 传入三个float64数据 返回一个float64数据
func pow(x, n, lim float64) float64 {
  // v变量只作用于if块内, 判断x^n是否小于lim
	if v := math.Pow(x, n); v < lim {
		return v
	} else {
		fmt.Printf("%g >= %g\n", v, lim)
	}
	return lim
}

func main() {
	fmt.Println(
		pow(3, 2, 10),
		pow(3, 3, 20),
	)
}
```

## switch

```go
package main

import (
	"fmt"
	"runtime"
)

func main() {
	fmt.Print("Go runs on ")
	switch os := runtime.GOOS; os {
	case "darwin":
		fmt.Println("OS X.")
	case "linux":
		fmt.Println("Linux.")
	default:
		// freebsd, openbsd,
		// plan9, windows...
		fmt.Printf("%s.\n", os)
	}
}
```

## defer

> 函数返回后才会执行

```go
package main

import "fmt"

func main() {
	fmt.Println("counting")

	for i := 0; i < 10; i++ {
		defer fmt.Println(i)
	}

	fmt.Println("done")
}
```

## 作业

1. 初始化名为`learn-go`的项目
2. 新建名为`utils`的包
3. 在包中实现三个函数
    - `*`号打印金字塔
    - 打印九九乘法表
    - 计算斐波那契数列, 传入计算位数, 输出值
4. 在main函数中调用这三个函数