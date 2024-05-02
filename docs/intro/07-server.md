> 将自我介绍页挂起来吧

## 代码

### 前端

1. `index.html`

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>自我介绍</title>
    <link rel="stylesheet" href="style.css" />
    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
  </head>

  <body>
    <h1>你好呀👋</h1>
    <h2>
      My name is
      <span id="name">加载中...</span>
      <span id="sex"></span>
    </h2>
    <p id="intro"></p>
    <p id="about">加载中...</p>
    <script src="app.js"></script>
  </body>
</html>
```

2. `style.css`

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

3. `app.js`

```js
$.getJSON('http://' + document.domain + ':8080/info', function (json) {
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

### 后端

1. `main.py`

```python
from flask import Flask
from flask_cors import CORS

# 新建服务
server = Flask("app")

CORS(server, supports_credentials=True)

# 定义路由
@server.route('/')
def index():
    return 'Hello Flask!'

# 定义路由
@server.route('/info')
def get_info():

    # 读取文件
    # file = open('info.json','r',encoding='utf-8')
    # data = file.read()
    # file.close()

    # 更高级的方式
    with open('info.json', 'r', encoding='utf-8') as f:
        data = f.read()

    return data

# 开启服务
server.run('0.0.0.0', port=8080)
```

2. `info.json`

```json
{
  "name": "fzf404",
  "sex": 1,
  "intro": "大一学生，就读于沈阳理工大学物联网专业。",
  "about": "是修炼中的全栈开发者，左派社会主义接班人，理想主义建政带师。社会化抚养推动者，继承制及死刑的反对者。轨道交通迷。"
}
```

## 将自我介绍页挂起来吧

> 白嫖地址 (困难)：[阿里云两周服务器](https://developer.aliyun.com/plan/student)
>
> 9 元 / 月：[华为云学生机](https://developer.huaweicloud.com/campus)
>
> 27 元 / 3 月：[腾讯云学生机](https://cloud.tencent.com/act/campus)

### 服务器配置

> 目前用户所接触到的都是内网 IP
>
> 只有云服务器才拥有公网 IP

1. 注册华为云账号
2. 下载 `华为云` APP 进行实名认证
3. 购买 9/mon 的云服务器，操作系统选择为为 `Debian`

> 我们将使用 debian10 作为服务器系统

4. 进入 `控制台` -> 选择 `乌兰察布` -> 进入 `弹性云服务器ECS`
5. 进入 `安全组` -> 点击 `Sys-default` -> 点击 `更改安全组规则`

> 默认只打开 80 端口，但后端需要用到 8080 端口

6. `入站方向规则` -> 添加 `8080`
7. 点击 `远程登录` —> 重置密码
8. 输入用户名 `root`，密码为刚才设置的密码

### 部署过程

```bash
# 查看当前路径
pwd
# 查看当前文件夹内容
ls
# 切换文件夹
cd

# 更新软件源列别
apt update -y

# 安装git
apt install git -y

# clone代码
git clone https://gitee.com/xxx/general-code.git

# 部署前端
cd general-code/07-部署到服务器/web

# 暂时部署
python3 -m http.server 80
# 后台部署
nohup python3 -m http.server 80 &
# 查看日志
cat nohup.out

# 查看服务开启情况
ps -ef | grep python3

# 停止服务
kill xxx

# 部署后端
# 安装 pip
apt install python3-pip

# 安装依赖
pip3 install flask flask_cors

# 进入并部署
cd ./general-code/07-部署到服务器/end

# 暂时部署
python3 main.py
# 持续部署
nohup python3 main.py &
```

## 课后

### 作业

1. 将目前自己写过的代码进行整理，推送到 Gitee
2. 部署到自己的服务器
