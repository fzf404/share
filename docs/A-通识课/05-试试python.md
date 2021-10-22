> python基础
>
> flask后端开发

## Python基础

> 互联网上最热门的编程语言。
>
> [下载地址](https://www.python.org/downloads/windows/)
>
> 版本：`3.8.10 win-64`

```python
# 进入交互式界面
$ python
>>> print('hello world')
helloworld
>>> answer = input("你的名字：")

# Ctrl + Z 后按Enter，退出交互界面

# 数据类型
a_num = 404
type(a_num)

a_str = "这是一个字符串"
a_str[4]
a_str[1:4]	# 第二个字符到第四个字符
type(a_str)

# 列表
a_list = ["你好", 'π', "你的值为: ", 3.14]	
type(a_str)	# 类型
a_list[0]	# 第1个值, 与c语言数组一样
a_list[0:3]	# 第1个到第3个值
a_list[2:] # 第2个值到最后一个值

a_dict = { "name": "fzf404", "age":19 }		# 字典
type(a_dict)
a_dict['name']	# 取值


# 循环
while True:
  print('hello world')
  print('你好世界')
print('世界不好')
  
# 条件循环
i = 10
while i > 0:
  print("倒数10下: ", i)
  i-=1		# i=i-1
  
# 条件判断
answer = input("你是猪吗？")
if answer == '是':
  print("真可爱")
elif answer == 'yes':
  print("so cute")
else:
  print("肮脏的人类")
  
  
# 引入扩展包
import math
import time
import json

# 可以在任意位置写语句
a_list = ["你好", 'π', "你的值为: ", math.pi]

# for 循环
print("计时开始")
for i in range(0, 10):
  print(i)
  time.sleep(1)
  
# 类型转换
str(404)
list(range(0,10))
          
# 遍历列表
for i in a_list:
  print(i)
  
# 函数
def add(a, b):
  return a + b
  
  
# 打开文件
json_file = open('info.json','r',encoding='utf-8')

# 读取文件为字符串
json_data = json_file.read()
# 字符串转字典
json_dict = json.loads(json_data)
# 字典取值
json_dict["name"]

# 关闭文件
json_file.close()
```

### 语法特点

1. 弱类型语言，无需指定变量类型就可以使用变量
2. 使用缩进确认代码归属，无需大括号和分号

## 写个接口吧

> 使用`flask`写后端
>
> 安装第三方库：`pip install flask`

### Hello

> 启动：`python 01-hello.py`

```python
from flask import Flask

server = Flask('app')

@server.route('/')
def index():
  return 'Hello Flask!'

server.run()

'''
 * Serving Flask app 'app' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
'''
```

### Info

```python
from flask import Flask

# 新建服务
server = Flask("app")

# 发送的数据
data = {
    "name": "王山而",
    "sex": 0,
    "intro": "大一学生，就读于沈阳理工大学物联网专业。",
    "about": "身体健康，大脑健全，心态良好，反诈骗能力高。啥都不会，进去想学东西的，emmmm没了。"
}

# 第二种方式
file = open('info.json','r',encoding='utf-8')
data = json_file.read()
file.close()


# 定义路由
@server.route('/')
def index():
    return 'Hello Flask!'

# 定义路由
@server.route('/info')
def get_info():
    return data

# 开启服务
server.run('127.0.0.1', port=8080)


# 前端修改请求地址
http://127.0.0.1:8080/info
```

### csv文件

> 以纯文本格式存储表格内容
>
> vscode插件：`Rainbow CSV`

- 存至：`data.csv`

```sql
2010020115,孟祥瑞,0,一枚艺术生，就读于沈阳理工大学动画专业。,是修炼中的全栈开发者，左派社会主义接班人，理想主义建政带师。社会化抚养推动者，继承制及死刑的反对者。轨道交通迷。
2010020116,王山而,1,大一学生，就读于沈阳理工大学艺术设计专业。,身体健康，大脑健全，审美良好，抗压能力强。啥都不会，进去想学东西的，emmmm没了。
```

#### 读取文件

```python
import csv

data_path = 'data.csv'

# 打开csv文件
file_csv = open(data_path, 'r', encoding='utf-8')

# 读取csv内容为str
# str_csv = file_csv.read()

# 将内容解析出来
object_csv = csv.reader(file_csv)	# 可以使用for遍历

# 关闭文件
file_csv.close()

# 转换为二维列表
list_csv = list(object_csv)

# 遍历列表
for item in list_csv:
  print("学号：", item[0])
  print("姓名：", item[2])
  print("源信息：", item)
```

### 获取前端传来的信息

```python
import csv
from flask import Flask, request

server = Flask('app')

data_path = 'data.csv'

@server.route('/info')
def get_info():
  
  # 获得url中的id
  user_id = request.args.get('id')
  
  print("用户ID：", user_id)
  
  # 所有接口必须有返回值
  return 'Test Get ID'
```

### 完成接口

```python
import csv
from flask import Flask, request

server = Flask('app')

data_path = 'data.csv'

@server.route('/api/info')
def get_info():
  # 获得url中的id
  user_id = request.args.get('id')
  
  # 打开文件
  file = open(data_path, 'r', encoding='utf-8')
  # 转换为列表
  data = csv.reader(file)
  # 关闭文件
  file.close()
  
  # 更简单的方法
  with open(data_path, 'r', encoding='utf-8') as f:
    data = csv.reader(file)

  for item in data:
    if item[0] == user_id:
      return {
          "name": item[1],
          "sex": item[2],
          "intro": item[3],
          "about": item[4]
      }
    
  # 没有匹配，则返回空
  return {
    "name": None,
    "sex": None,
    "intro": None,
    "about": None
  }

# 开启服务
server.run('127.0.0.1', port=8080)
```

## 课后

### 作业

1. 使用python打印九九乘法表
2. 完成自我介绍页的前后端，传至Gitee

### 推荐阅读

[python基础知识总结](https://zhuanlan.zhihu.com/p/56595142)

[2333一个挺有趣的flask教程](https://zhuanlan.zhihu.com/p/73278003)
