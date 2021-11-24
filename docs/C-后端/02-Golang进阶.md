> go的更多语法

## 数组、切片与映射

### 数组

> 长度不可改变

```go
// 数组
var a [3]int
a := [3]int{1,2,3}	// 复合字面值初始化
a := [...]string{
    "123",
    "234",
    "345"
}

// 循环遍历
for i :=0 ; i < len(a); i++ {
    fmt.Print;n(a[i])
}
// range循环
for index,data := range a {
  fmt.Println(index,data)
}
```

### 切片

> 长度可变

```go
// 切片 可变长数组
var b = []string{"1","2","3"}
b := []string{"1","2","3"}
b = b.append(b,"4")
bs = b[1:2]		// q'w
// for循环遍历数组
for k, v := range b {
    fmt.Println(k, v)
}
// Out
0 1
1 2
2 3
3 4
```

### 映射

```go
// 映射：字典or键值对
// 使用make创建map对象
items := make(map[string]int)
// 对象赋值
items["first"] = 1
items["mid"] = 2
items["last"] = 4
// 删除键值对 
delete(items, "mid")
// 快速创建
payload := map[string]interface{}{
  "UserName": req.UserName,
}
// 遍历
for k, v := range items {
    fmt.Println(k, v)
}
```

## 结构体及方法

```go
// 定义变量类型
type myFloat float64

// 定义结构体
type myFriend struct {
	name string
	age  int
}

// 为结构体定义方法
// func(变量名 结构体名) 方法名()
func (getone myFriend) showName() {
	fmt.Println(getone.name)
}
// 使用指针修改值
func (getone *myFriend) setAge(newAge int){
	(*getone).age = newAge
}

func main() {
	newPerson := MyFriend{name: "fzf", age: 18}
	fmt.Println(newPerson)
    // {fzf 18}
    newPerson.showName()
    // fzf
    newPerson.setAge(20)
    fmt.Println(newPerson)
    // {fzf 20}
}
```

## 接口

```go
package main

import "fmt"

// 定义接口 内部两个方法
type Phone interface {
    call(param int) string
    takephoto()
}

// 结构体实例
type Xiaomi struct {}

// 为Xiaomi定义call方法
func (mi Xiaomi) call(param int) string{
    fmt.Println("I'm Xioami, Calling: ", param)
    return "Hang up..."
}

func (mi Xiaomi) takephoto() {
    fmt.Println("I take a photo.")
}

func main(){
    // 新建接口
    var phone Phone
    // 接口获得一个结构体
    phone = new(Xiaomi)
    // 调用结构体接口的方法
    phone.takephoto()
    // 调用带参数的方法
    r := phone.call(404)
    fmt.Println(r)
}
/*
I take a photo.
I'm Xioami:  404
I'm death
*/
```

## 作业

1. 完成此函数

    ```go
    /**
     * @description: 向切片指定位置插入值
     * @param {[]int8} source 源切片
     * @param {int} postion 插入位置
     * @param {[]int8} value 需要插入的切片
     * @return {[]int8} 返回值
     */
    func SliceInsert(source []int8, postion int, value []int8) []int8 {
      
    }
    ```

