> HTML、CSS、JavaScript

!!! note Note

    教案网址增加亮色模式啦！

### 如何截屏

> 截屏：++win+shift+s++
>
> 剪贴板历史：++win+v++

## 不为人知的浏览器

> 浏览器的复杂性不亚于操作系统
>
> 推荐使用 Edge 浏览器

### DevTools

> 浏览器为开发者提供的调试工具

- 浏览器向服务器发送请求，接收到网页源码，渲染到屏幕上
- 使用 DevTools (开发者工具) 可以看到这一过程

#### 使用

- 使用键盘上 ++f12++ / ++ctrl+shift+c++ 打开控制台
- 点击左上角的 `元素检查`，修改网站内容，查看效果，如果可以，则修改代码
- 观察网页结构
    - 语法像标签一样，使用 `<xxx>` 括起来，并且还有闭合标签 `</xxx>`
    - 最外层 `<html>....</html>`
    - `<html>` 标签内部有 `<head>` 及 `<body>`
    - 只有标签包起来的东西，才会在页面中显示

## 写一个自我介绍页吧

> 为这个项目花了很多心思，如何用最简单的样式做出简洁美观的网页
>
> 参考 [EvanYou](https://evanyou.me/) 的首页

## 网页的骨架

> 来写 HTML 吧 (Hyper Text Markup Language)

- HTML 是一种标签语言
- 使用标签将内容包裹住
- 浏览器根据国际标准，将内部的内容按照标签展示出来
- 保存位置：`C:\Users\<UserName>\Work\intro\03-intro.html`
- 格式化代码：++alt+shift+f++
- 预览：安装插件：`Live Server`，右下角 `go live`

```html
<body>
  <h1>你好呀 👋</h1>
  <h2>My name is 孟祥瑞 👦</h2>
  <p>一枚艺术生，就读于沈阳理工大学动画专业</p>
  <p>
    是修炼中的全栈开发者，左派社会主义接班人，理想主义建政带师，社会化抚养推动者，继承制及死刑的反对者
  </p>
</body>
```

## 网页的皮肉

> 来写样式表吧！
>
> 样式表有很多关键字，熟练掌握需要长时间的训练

- 保存位置：`C:\Users\<UserName>\Work\intro\04-style.html`

### 选择器

```html
<style>
  /* 选择h1标签  */
  h1 {
    color: black;
    font-size: 12px;
  }
  /* 选择id为hi的标签 */
  #hi {
    color: blue;
  }
  /* 选择class为hello的标签 */
  .hello {
    color: red;
  }
</style>

<h1>你好呀👋</h1>
<h1 id="hi">你不好呀👋</h1>
<h1 class="hello">你一点不好呀👋</h1>
```

- `id` 是唯一的
- `class` 可以是多个的
- `css` 每条样式需要用分号分隔

### 颜色表示法

> 只需要 RGB 三个颜色的灯泡，就可以组合出人眼能分辨的所有颜色

```css
/* 十六进制表示法 */
/* 000000 - ffffff */
color: #000000;
color: #454545;
color: #999999;
color: #ffffff;

color: #aa0000;
color: #00aa00;
color: #0000aa;

/* RGB表示法 */
color: rgb(0, 0, 0);
color: rgb(100, 100, 100);
color: rgb(255, 255, 255);

color: rgb(100, 0, 0);
color: rgb(0, 100, 0);
color: rgb(0, 0, 100);

/* RGBA表示法 */
color: rgba(100, 0, 0, 0.9);
color: rgba(100, 0, 0, 0.5);
color: rgba(100, 0, 0, 0.2);
```

### 盒模型

```html
<style>
  h1 {
    /* 边框 */
    border: #454545 solid 5px;
    border-radius: 10px;

    /* 内边距 */
    padding: 15px;
    padding: 15px 30px;
    /* padding-top: 15px; */
    /* padding-bottom: 15px; */
    padding-left: 100px;
    /* padding-right: 100px; */

    /* 外边距 */
    margin: 50px;
    margin: 50px 100px;
    margin-left: 200px;
    margin-right: 200px;
  }
</style>

<h1>你好呀👋</h1>
```

### 美化一下咱们的网页吧

> 新建：`C:\Users\<UserName>\Work\intro\05-style.css`
>
> 将样式表放入新文件：`05-style.css`
>
> 引入：`<link rel="stylesheet" href="05-style.css">`

```css
body {
  /* 内边距 */
  padding: 10vh 10vw;
}

h1 {
  /* 文字大小 */
  font-size: 3em;
  margin-bottom: 0.8em;
}

h2 {
  font-size: 2em;
  margin-bottom: 1.4em;
}

p {
  font-size: 1.4em;
  /* 字体粗细 */
  font-weight: 300;
  /* 行高 */
  line-height: 1.6em;
  /* 最大宽度 */
  max-width: 600px;
}
```

## 动态的网页

> 让网页动起来吧

### JavaScript

> JS 与 Java，就像雷锋与雷峰塔的区别
>
> 可以直接在浏览器控制台写 JS 代码

```js
// 只讲解ES6标准推荐的写法

// 变量
let a = 404
// a 的数据类型
typeof a
// 字符串
a = '404' // 与 a = "404" 一样
typeof a

// 常量
const b = 404
typeof b
b = '404' // 报错

// 对象 object
let obj = { name: 'fzf', age: 19 }
typeof obj
obj.name
obj.age = 18

// 条件判断
if (a == 404) {
  console.log('a is 404')
} else {
  console.log('a is not 404')
}

// for循环
for (let i = 0; i < 10; i++) {
  console.log(i)
}

// 函数
// 不需要指定返回类型及传入数据的类型
function add(a, b) {
  return a + b
}
```

### JSON

> 十分常用的数据存储格式
>
> 浏览器解析 JSON 的插件：`FeHelper`
>
> [B 站 API (其他网站也是)](https://api.bilibili.com/pgc/web/season/home/top)
>
> VSCode 配置文件

#### 观察格式

- `{ ... }`：最外层
- `{ "code": 123 }`：键值对 (key：value)
- `{ "list": [ 1, 2, 3] }`：键值对里的值为列表

#### 精简为 JSON 文件

> 将需要自我介绍的信息精简为 `07-info.json` 文件

```json
{
  "name": "张三",
  "sex": 0,
  "intro": "大一学生，就读于沈阳理工大学物联网专业",
  "about": "身体健康，大脑健全，心态良好，反诈骗能力高，剩下啥都不会"
}
```

### jQuery

> JS 库，让网页操作变得更简单

- jQuery 为我们提供了封装好的 API (应用程序编程接口)
- 我们不需要关注内部的实现原理，就可以简单的操作网页内容

#### 基础

- [BootCDN](https://www.bootcdn.cn/)

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Hello jQuery</title>
    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.6.0/jquery.js"></script>
  </head>

  <body>
    <h1>你好呀 👋</h1>
    <h2>
      My name is
      <span id="name">孟祥瑞</span>
      👦
    </h2>
    <p>一枚艺术生，就读于沈阳理工大学动画专业</p>
    <p>
      是修炼中的全栈开发者，左派社会主义接班人，理想主义建政带师，社会化抚养推动者，继承制及死刑的反对者
    </p>

    <script>
      $('#name').text('王山而')
    </script>
  </body>
</html>
```

- JS 代码要写在页面内容后，因为代码是一行一行执行的

#### 加载 JSON 文件

- 保存位置：`C:\Users\<UserName>\Work\intro\06-app.js`

```js
$.getJSON('info.json', function (json) {
  $('#name').text(json.name)
  $('#intro').text(json.intro)
  $('#about').text(json.about)

  // 0为女生，1为男生
  if (json.sex == '1') {
    $('#sex').text('👦')
  } else {
    $('#sex').text('👧')
  }
})
```

## 代码规范

1. 缩进对齐
2. 变量名符合正常人阅读规范

## 成品代码

### `03-intro.html`

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>自我介绍</title>
    <link rel="stylesheet" href="05-style.css" />
    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
  </head>

  <body>
    <h1>你好呀 👋</h1>
    <h2>
      My name is
      <span id="name">fzf</span>
      <span id="sex">👦</span>
    </h2>
    <p id="intro">一枚艺术生，就读于沈阳理工大学动画专业</p>
    <p id="about">
      是修炼中的全栈开发者，左派社会主义接班人，理想主义建政带师，社会化抚养推动者，继承制及死刑的反对者
    </p>
    <script src="app.js"></script>
  </body>
</html>
```

### `05-style.css`

```css
body {
  /* 内边距 */
  padding: 10vh 10vw;
}

h1 {
  /* 文字大小 */
  font-size: 3em;
  margin-bottom: 0.8em;
}

h2 {
  font-size: 2em;
  margin-bottom: 1.4em;
}

p {
  font-size: 1.4em;
  /* 字体粗细 */
  font-weight: 300;
  /* 行高 */
  line-height: 1.6em;
  /* 最大宽度 */
  max-width: 600px;
}
```

### `06-app.js`

```js
$.getJSON('06-info.json', function (json) {
  $('#name').text(json.name)
  $('#intro').text(json.intro)
  $('#about').text(json.about)

  // 0为女生，1为男生
  if (json.sex == '1') {
    $('#sex').text('👦')
  } else {
    $('#sex').text('👧')
  }
})
```

### `07-info.json`

```json
{
  "name": "张三",
  "sex": 1,
  "intro": "大一学生，就读于沈阳理工大学物联网专业",
  "about": "身体健康，大脑健全，心态良好，反诈骗能力高，剩下啥都不会"
}
```

## 课后作业

1. 根据课程内容，写一个自己的自我介绍页
2. 使用 Markdown 语法写一篇笔记，命名为 `README.md`

### 推荐阅读

[HTML - 菜鸟教程](https://www.runoob.com/html/html-tutorial.html)

[CSS - 菜鸟教程](https://www.runoob.com/css/css-tutorial.html)

[jQuery - 菜鸟教程](https://www.runoob.com/jquery/jquery-tutorial.html)
