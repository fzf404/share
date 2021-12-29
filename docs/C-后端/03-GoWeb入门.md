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

