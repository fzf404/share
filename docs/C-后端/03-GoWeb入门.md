> [参考教案](https://github.com/astaxie/build-web-application-with-golang/blob/master/zh/SUMMARY.md)

## GoRoutine

```go
package main

import (
	"fmt"
	"runtime"
	"time"
)

func showNumber(i int) {
	runtime.Gosched()
	fmt.Println(i)
}

func main() {

	for i := 0; i < 10; i++ {
		go showNumber(i)
	}

	fmt.Println("Haha")
	time.Sleep(50000)
}
```

## Channel

```go
package main

import "fmt"

func sum(a []int, c chan int) {
	total := 0
	for _, v := range a {
		total += v
	}
	c <- total  // send total to c
}

func main() {
	a := []int{7, 2, 8, -9, 4, 0}

	c := make(chan int)
	go sum(a[:len(a)/2], c)
	go sum(a[len(a)/2:], c)
	x, y := <-c, <-c  // receive from c

	fmt.Println(x, y, x + y)
}
```

### Web基础

```go
package main

import (
	"fmt"
	"log"
	"net/http"
	"strings"
)

func sayhelloName(w http.ResponseWriter, r *http.Request) {
	r.ParseForm()
	for k, v := range r.Form {
		fmt.Fprintf(w, "key: "+k+" value: "+strings.Join(v, ""))
	}

}

func pong(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "pong")
}

func main() {
	// 为特定路径的访问指定处理函数
	http.HandleFunc("/", sayhelloName)
	http.HandleFunc("/ping", pong)
	// 运行前提示
	log.Println("Server Runing on http://127.0.0.1:8080")
	// 开始服务
	err := http.ListenAndServe(":8080", nil)
	// 错误处理
	if err != nil {
		log.Fatal("ListenAndServe: ", err)
	}
}
```

### 表单基础

```go
package main

import (
	"fmt"
	"html/template"
	"log"
	"net/http"
)

func sayhelloName(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Hello astaxie!") //这个写入到w的是输出到客户端的
}

func login(w http.ResponseWriter, r *http.Request) {
	r.ParseForm()
	fmt.Println("method:", r.Method) //获取请求的方法
	if r.Method == "GET" {
		t, _ := template.ParseFiles("login.gtpl")
		log.Println(t.Execute(w, nil))
	} else {
		//请求的是登录数据，那么执行登录的逻辑判断
		fmt.Println("username:", r.Form["username"])
		fmt.Println("password:", r.Form["password"])

		if r.Form["username"][0]=="fzf" && r.Form["password"][0]=="123456"{
			//为空的处理
			fmt.Fprintf(w, "登录成功") 
			return
		}
		fmt.Fprintf(w, "登录失败") 
	}
}

func main() {
	http.HandleFunc("/", sayhelloName)       //设置访问的路由
	http.HandleFunc("/login", login)         //设置访问的路由
	err := http.ListenAndServe(":9090", nil) //设置监听的端口
	if err != nil {
		log.Fatal("ListenAndServe: ", err)
	}
}

```

[作业源码地址](https://qlstudio.coding.net/p/houduanjiaoxue/d/homework/git)

软件: Navicat
