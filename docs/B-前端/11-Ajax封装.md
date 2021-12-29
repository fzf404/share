# 关于原生 Ajax 封装

## 封装前 Ajax 展示

> 下文的写法适配 IE ，微软将在 2022 年 6 月 15 日停止对 IE 的服务。

**post**

```js
var baseUrl = "http://127.0.0.1:1880";
// 1.创建Ajax对象
var xhr = null;
try {
  xhr = new XMLHttpRequest();
} catch (error) {
  xhr = new ActiveXObject("Microsoft.XMLHTTP");
}
// 2.调用open
xhr.open("post", `${baseUrl}/test`, true);
// 必须在send方法之前设置请求头
xhr.setRequestHeader("content-type", "application/x-www-form-urlencoded");
/* post提交的数据需要通过send方法进行提交 */
// 3.调用send
xhr.send("username=yyy&age=19");
// 4.等待数据响应
xhr.onreadystatechange = function () {
  if (xhr.readyState == 4) {
    // 判断状态码是否为200
    if (xhr.status == 200) {
      alert(xhr.responseText);
    } else {
      alert("Error:" + xhr.status);
    }
  }
};
```

**get**

```js
// 1.创建Ajax对象
var xhr = null;
try {
  xhr = new XMLHttpRequest();
} catch (error) {
  xhr = new ActiveXObject("Microsoft.XMLHTTP");
}
// 2.调用open
xhr.open("get", `${baseUrl}/test?username=yyy&age=19`, true);
// 3.调用send
xhr.send();
// 4.等待数据响应
xhr.onreadystatechange = function () {
  if (xhr.readyState == 4) {
    // 判断状态码是否为200
    if (xhr.status == 200) {
      alert(xhr.responseText);
    } else {
      alert("Error:" + xhr.status);
    }
  }
};
```

## 封装过程

**post**和**get**有很多重复的部分，保留重复的部分，不同的用 _if_ 判断就可以了。

```js
try {
  xhr = new XMLHttpRequest();
} catch (error) {
  xhr = new ActiveXObject("Microsoft.XMLHTTP");
};

......

xhr.onreadystatechange = function() {
  if (xhr.readyState == 4) {
    if (xhr.status == 200 && success) {
      success(xhr.responseText);
    } else if (error) {
      error("Error" + xhr.status);
    };
  };
};
```

**post**和**get**第一个区别在于数据的拼接方式不同。

> PS：上文的路径写起来比较麻烦，下文简写为 **url**，即 **`url = baseUrl + '/test'`**。

**get**

```js
xhr.open("get", url + "?" + data, true);
```

**post**

```js
xhr.open("post", url, true);

......

xhr.send(data);
```

除此之外 **post** 方法还需要设置请求头，以保证数据的正确传输。\
即

```js
xhr.open("post", url, true);

xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");

xhr.send(data);
```

所以这一段需要先做一个判断，在这里我就用 _if_ 进行判断了，因为比较简单。\
先判断 **get** 方法下是否有数据，如果有就进行拼接。

```js
if (method == "get" && data) {
  url += `?${data}`;
  // 可以在这里添加一个打印，查看url是否正确拼接
  console.log(url);
}
xhr.open(method, url, true);
```

数据拼接完成了，接下来是对方法的判断。

```js
if (method == "get") {
  xhr.send();
} else {
  if (header) {
    for (const item in header) {
      xhr.setRequestHeader(item, header[item]);
    }
  } else {
    xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
  }
  xhr.send(data);
}
```

再把这些部分进行组装。

```js
var xhr = null;
try {
  xhr = new XMLHttpRequest();
} catch (error) {
  xhr = new ActiveXObject("Microsoft.XMLHTTP");
}
if (method == "get" && data) {
  url += `?${data}`;
  console.log(url);
}
xhr.open(method, url, true);
if (method == "get") {
  xhr.send();
} else {
  if (header) {
    for (const item in header) {
      xhr.setRequestHeader(item, header[item]);
    }
  } else {
    xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
  }
  xhr.send(data);
}
xhr.onreadystatechange = function () {
  if (xhr.readyState == 4) {
    if (xhr.status == 200 && success) {
      success(xhr.responseText);
    } else if (error) {
      error("Error" + xhr.status);
    }
  }
};
```

接下来就是定义函数了，这里有个问题待会再说。

```js
function $ajax(method, url, header, data, success, error) {
  var xhr = null;
  try {
    xhr = new XMLHttpRequest();
  } catch (error) {
    xhr = new ActiveXObject("Microsoft.XMLHTTP");
  }
  if (method == "get" && data) {
    url += `?${data}`;
    console.log(url);
  }
  xhr.open(method, url, true);
  if (method == "get") {
    xhr.send();
  } else {
    if (header) {
      for (const item in header) {
        xhr.setRequestHeader(item, header[item]);
      }
    } else {
      xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
    }
    xhr.send(data);
  }
  xhr.onreadystatechange = function () {
    if (xhr.readyState == 4) {
      if (xhr.status == 200) {
        if (success) {
          success(xhr.responseText);
        }
      } else {
        if (error) {
          error("Error" + xhr.status);
        }
      }
    }
  };
}
```

这样写看似没有问题，但是会把参数写死，顺序不可改变。所以我们需要将其改为对象形式，就会灵活很多。

```js
function $ajax({ method, url, header, data, success, error }) {
  var xhr = null;
  try {
    xhr = new XMLHttpRequest();
  } catch (error) {
    xhr = new ActiveXObject("Microsoft.XMLHTTP");
  }
  if (method == "get" && data) {
    url += `?${data}`;
    console.log(url);
  }
  xhr.open(method, url, true);
  if (method == "get") {
    xhr.send();
  } else {
    if (header) {
      for (const item in header) {
        xhr.setRequestHeader(item, header[item]);
      }
    } else {
      xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
    }
    xhr.send(data);
  }
  xhr.onreadystatechange = function () {
    if (xhr.readyState == 4) {
      if (xhr.status == 200) {
        if (success) {
          success(xhr.responseText);
        }
      } else {
        if (error) {
          error("Error" + xhr.status);
        }
      }
    }
  };
}
```

我们还可以将 _method_ 进行一个初始化，让它默认等与 _get_ 这样就可以再方便许多。\
于是，它便诞生了。

## 完成展示

```js
function $ajax({ method = "get", url, data, success, error }) {
  var xhr = null;
  try {
    xhr = new XMLHttpRequest();
  } catch (error) {
    xhr = new ActiveXObject("Microsoft.XMLHTTP");
  }
  if (method == "get" && data) {
    url += `?${data}`;
    console.log(url);
  }
  xhr.open(method, url, true);
  if (method == "get") {
    xhr.send();
  } else {
    xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
    xhr.send(data);
  }
  xhr.onreadystatechange = function () {
    if (xhr.readyState == 4) {
      if (xhr.status == 200) {
        if (success) {
          success(xhr.responseText);
        }
      } else {
        if (error) {
          error("Error" + xhr.status);
        }
      }
    }
  };
}
```

在应用的时候，只需要这样调用就可以了。

```js
$ajax({
  method: "post",
  url: "",
  data: "",
  success: function (result) {},
  error: function (result) {},
});
```

至此，**大功告成**！
