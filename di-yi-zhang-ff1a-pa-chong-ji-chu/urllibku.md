## **url库：**

url库是Python中的一个基本库，可以模拟浏览器的行为，并且url的所有网络请求方法都被集成到`url.request`模块下面

## url库的引入方法：

```py
from urllib import request

url = ("http://www.baidu.com")
resp = request.urlopen(url)
print(resp.read())
```

1，`url`：请求`url`

2，`data`：请求的`date`，如果设置了这个值那么成为`post`请求。

3，返回值：返回值是一个`http.client.THHPresponse`对象，这个对象是一个类文件句柄对象。

有`read(size)`、`readline`、`readlines`、以及`getcode`等方法。

## urlretrieve函数：

urlretrieve函数可以方便的将网页上的一个文件保存到本地，以下是将百度保存到本地的一个例子。

```py
from urllib import request
request.urlretrieve(http://www.baidu.com,baidu.html)
```

其中`http://www.baidu.com`是`url`，`baidu.html`是保存到本地的文件为`baidu.html`

## urlencode函数：

用浏览器发送请求的时候，如果url中包含中文或者其他特殊字符，那么浏览器会自动编码，如果使用代码发送请求，那么需要手动编码，这时候就需要用`urlencode`函数来实现,`urlencode`可以吧字典数据转换成URL编码数据。实例如下：

```py
from urllib import parse
data = {name:"爬虫数据","greet":"Hello World","age":10}
qs = parse.urlencode{data}
print(qs)
```

## parse\_qs函数:

可将经过编码后的URL进行解码。实例如下:

```py
from urllib import parse
qs = "已经编码的URL"
print(parse.parse_qs(qs))
```



