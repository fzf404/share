> python基础
>
> win32API

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
  print("倒数s: ", i)
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

## 保存数据

## 简单的接口


## 课后

### 作业

### 推荐阅读
