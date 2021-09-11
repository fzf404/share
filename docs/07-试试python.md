# 07-试试python

> python基础
>
> win32API

## Python基础

> 一门新的脚本语言

```python
# 进入交互式界面
$ python3
>>> print('hello world')
helloworld

# 使用 IDLE

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
  print("倒数: ", i)
  i-=1		# i = i-1
  
# 条件判断
answer = input("你是猪吗？")
if answer == '是':
  print("真可爱")
elif answer == 'yes':
  print("so cute")
else:
  print("肮脏的人类")
  
# 引入第三方包
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

### 爬一下b站热榜

### requests

> [官方文档](https://docs.python-requests.org/zh_CN/latest/)

```python
import requests

url = 'https://api.bilibili.com/x/web-interface/ranking/v2'
res = request.get(url)	# 请求该网址

res_json = res.json()		# 解码转换为字典

# 打印所有视频标题
for i in res_json['data']['list']:
  print(i['title'])
```

### win32API

```python
import win32gui
import win32con
import win32clipboard as cb
import time

def send(name, msg):
    cb.OpenClipboard()    # 打开剪贴板
    cb.SetClipboardData(win32con.CF_UNICODETEXT, msg)       # 设置剪贴板内容
    cb.CloseClipboard()     # 关闭剪贴板
    # 获取qq窗口句柄
    handle = win32gui.FindWindow(None, name)
    if handle == 0:
        print('未找到窗口！')
    # 显示窗口
    win32gui.ShowWindow(handle, win32con.SW_SHOW)
    # 把剪切板内容粘贴到qq窗口
    win32gui.SendMessage(handle, win32con.WM_PASTE, 0, 0)
    # 按下后松开回车键，发送消息
    win32gui.SendMessage(handle, win32con.WM_KEYDOWN, win32con.VK_RETURN, 0)
    win32gui.SendMessage(handle, win32con.WM_KEYUP, win32con.VK_RETURN, 0)
    time.sleep(1)  # 延缓进程

def main():
    name = '你们的小f'  # QQ聊天窗口的名字
    print('开始')
    for i in range(1, 6):
        send(name, '第'+str(i)+'次测试')
    print('结束')

main()
```

## 课后

### 作业

### 推荐阅读
