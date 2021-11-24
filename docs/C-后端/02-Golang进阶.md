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

1. 完成此函数(切片)

    ```go
    package main
    
    import "fmt"
    
    /**
     * @description: 向切片指定位置插入值
     * @param {[]int} source 源切片
     * @param {int} postion 插入位置
     * @param {[]int} target 需要插入的切片
     * @return {[]int} 返回值
     */
    func SliceInsert(source []int, postion int, target []int) []int {
    	// 提示: 新建result切片 使用for循环遍历source 当index==postion时 遍历taget, 将value插入result中
    }
    
    func main() {
    	source := []int{1, 4, 5, 6}
    	target := []int{2, 3}
    	fmt.Println(SliceInsert(source, 1, target))
    }
    
    /* 输出:
    [1 2 3 4 5 6]
    */
    
    ```

2. 完成此程序(闭包)

    ```go
    package main
    
    /**
    * @description: 求n的n次方
    */
    func square(n int64) func() int64 {
      // 提示: 很简单, 返回一个函数, 内部是n*n
    }
    
    func main() {
    	f := square(2)
    	for i := 0; i < 5; i++ {
    		// 将会打印n的n次方
    		println(f())
    	}
    }
    
    /*
    4
    16
    256
    65536
    4294967296
    */
    ```

3. 完成此程序(结构体及方法)

    ```go
    package main
    
    type Scores struct {
      chinese uint // 语文成绩
      math uint // 数学成绩
      english uint // 英语成绩
    }
    
    /*
     * TODO:
     * @description: 为Score结构体定义求成绩总和的方法
     * @param {Scores} s Scores结构体
     * @return {uint} 总成绩
    */
    func (s Scores) sum() uint {
      // 提示: 求三科成绩的总和
    }
    
    type Student struct {
    	id uint // 学号
    	name string // 姓名
      scores Scores // 成绩 
    }
    
    /**
     * TODO:
     * @description: 找出切片中成绩最高的同学
     * @param {[]Student} students 全部学生的切片
     * @return {Student} 最高分结构体
     */
    func No1(students []Student) Student {
    	// 定义空Student, 遍历Students切片, 查看成绩是否大于新建的Student, 大于则覆盖,不大于则下一个
    }
    
    
    func main(){
      // 新建三个同学
      students := []Student{
        Student{2010020115,"王山而",Scores{96,84,90}},
    		Student{1903060321,"卢成朋",Scores{103,92,121}},
    		Student{1903060320,"王海燕",Scores{99,113,103}},
      }
    	// 遍历每个同学, 打印出他们的分数
    	for _,student := range students {
    		println(student.name,": ",student.scores.sum())
    	}
    	// 计算最高分并打印
    	print("最高分为: ", No1(students).name)
    }
    ```

    

