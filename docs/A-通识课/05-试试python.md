> python基础
>
> flask后端开发

## Python基础

> 一门新的脚本语言

```python
# 进入交互式界面
$ python
>>> print('hello world')
helloworld

# 数据类型
a_str = "这是一个字符串"
a_num = 404
a_list = ["你好", 'π', "你的值为: ", math.pi]

# 循环
while True:
  print('hello world')
  
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

# for 循环
print("计时开始")
for i in range(0, 10):
  print(i)
  time.sleep(1)
          
# 遍历列表
for i in a_list:
  print(i)
```

## 写个接口吧

```python
from flask import Flask, request

# 新建服务
server = Flask("first_flask")

# 发送的数据
data = {
    "name": "张大三",
    "sex": 0,
    "intro": "大一学生，就读于沈阳理工大学物联网专业。",
    "about": "身体健康，大脑健全，心态良好，反诈骗能力高。啥都不会，进去想学东西的，emmmm没了。"
}

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

## 课后



### 作业

### 推荐阅读
