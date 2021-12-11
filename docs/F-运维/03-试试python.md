### 爬一下 b 站热榜

> `pip install requests`
>
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
