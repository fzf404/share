> VBS 基本语法、CMD 基本命令

## Hello World

### 第一个程序

> 做一个 Hello World 弹框吧！

- 桌面 `鼠标右键` -> 点击 `新建文本文档`
- 修改输入法为英文模式
- 打开新建的文本文档，输入以下内容：

```VBScript
msgbox("Hello, World!")
```

- 点击左上角 `文件` -> 点击 `保存` / 按 `Ctrl + S`
- 右键单击文件 -> 点击 `重命名` / 按 `F2` -> 改为 `01-HelloWorld.vbs`
- 点击运行，弹出内容为 `HelloWorld` 的弹框
- 更改窗口位置：`Win + 方向左键`

#### 扩展名不显示？

- 按 `Win + E` 打开 `文件资源管理器`
- 在菜单栏中点击 `查看`
- 勾选右侧 `文件扩展名`

### 扩展名是什么

> 仅仅是一些字母的集合，修改了扩展名后，就变成了可运行的程序。

- 为什么要有扩展名？
  - 在不读取文件内容的情况下，系统无法得知该文件需要用什么软件打开

### 使用中文

1. 右键编辑 -> 修改内容为中文

```VBScript
msgbox("你好, 世界！")
```

2. 运行发现报错 / 乱码
3. 百度寻找解决办法

## VBS 语法

### 循环

> 如何恶搞用户，让他关不掉这个窗口呢？
>
> 脚本语言的代码是一行一行执行的。
>
> 每次关掉后执行下一行代码。

```VBScript
' 写入无限多的 msgbox
msgbox("你好, 世界！")
msgbox("你好, 世界！")
msgbox("你好, 世界！")
```

有没有更简单的方法？

```VBScript
' 这是一行注释, 用法如其名, 计算机不会执行这行东西
' 未来的编程之路将会经常用到他
do
  msgbox("关掉？你在想Peach")
loop
```

#### 如何关闭

1. 任务栏单击鼠标右键 / 按 `Ctrl + Alt + Del`
2. 选择 `任务管理器`
3. 找到 `MicroSoft ® ...` 并选中
4. 点击右下角 `结束任务` / 重启电脑

### 条件循环

> 倒数 10 个数的窗口。
>
> 每次运行前判断条件是否满足。

```VBScript
' 定义一个变量名字叫i, 值为10
dim i
' 这和数字怎么不需要"括起来呢？
' 只有字符串需要用"括起来
i=10

' 持续执行下面的代码, 直到i不大于0
do while i>0
  msgbox(i)
  i=i-1
loop

' = 等于
' <> 不等于
' > 大于
' < 小于
```

### 条件判断

> 加入恶搞用户的交互。
>
> 根据条件决定是否运行。

```VBScript
dim answer
' 一个输入框, 输入的结果命名为answer
answer = inputbox("说“我是猪”")

' 判断说输入的值是否为 我是猪
if answer = "我是猪" then
  msgbox("哈哈哈, 你是猪")
elseif answer = "I'm a pig" then
  msgbox("hahaha, you are a pig")
else
  do
    msgbox("你在想Peach")
  loop
end if
```

以上就是编程中最常用的三种表达式了

### 更多？

> 制作一个有破坏作用恶搞程序。
>
> 为类生产一个实例，并调用实例中的方法。
>
> 这些东西编程语言已经为你实现好了，我们所作的就是决定他的用用途。
>
> 未来能够自己编写类的时候，就可以理解了。

```VBScript
' 一个输入框, 输入的结果命名为answer
answer = inputbox("说“我是猪”")

' 判断说输入的值是否为“我是猪”
if answer = "我是猪" then
  msgbox("哈哈哈, 你是猪")
elseif answer = "I'm a pig" then
  msgbox("hahaha, you are a pig")
else
  ' 使用 set 创建一个可以调用的实例
  ' 汽车 = 制造(图纸)
  set ws = createobject("Wscript.shell")
  ' 汽车.发动('去曹县')
  ws.run("cmd.exe /c shutdown -s -t 10" )
  msgbox("10s后就会关机")
end if
```

## 课后

### 作业

1. 根据教案，实现一下课堂中的例子，并保存好代码。
2. 做一个小的恶搞程序，发给室友 / 同学，拍个小视频。

### 推荐阅读

[整蛊的 VBS 代码](https://zhuanlan.zhihu.com/p/142737363)

[VBS 基础语法整理](https://zhuanlan.zhihu.com/p/367897802)
