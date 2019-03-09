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

request.urlretrieve("http://www.baidu.com","baidu.html")
#request.urlretrieve("URL","保存的文件格式")必须为这中格式，必须URL和保存的文件格式必须要加上""
```

其中`http://www.baidu.com`是`url`，`baidu.html`是保存到本地的文件为`baidu.html`

## urlencode函数：

用浏览器发送请求的时候，如果url中包含中文或者其他特殊字符，那么浏览器会自动编码，如果使用代码发送请求，那么需要手动编码，这时候就需要用`urlencode`函数来实现,`urlencode`可以吧字典数据转换成URL编码数据。实例如下：

```py
from urllib import parse

#data赋值的是一个数组需要用上大括号{}且数组中的元素需要使用""
data = {"name":"爬虫数据","greet":"Hello World","age":10}
qs = parse.urlencode(data)
print(qs)
```

## parse\_qs函数:

可将经过编码后的URL进行解码。实例如下:

```py
from urllib import parse

qs = "已经编码的URL"
print(parse.parse_qs(qs)
```

## urlparse和urlsplit用法:

有时候拿到一个url，想对这个url各个组成部分进行分割，那么这个时候就可以用urlparse和urlsplit进行分割操作了，实例如下：

```py
from urllib import parse

url = "http://www.baidu.com/s?usernaem=Scrooge"
#urlparse用法和urlsplit想法基本相同，urlparse可获取params属性，而urlsplit则获取不到。
result = parse.urlparse(url)
#urlparse用法和urlsplit想法基本相同，urlparse可获取params属性，而urlsplit则获取不到。
#resul = parse.urlsplit(url)

print("scheme",result.scheme)
print("netloc",result.netloc)
print("path",result.path)
print("params"result.params)
print("query",result.query)
print("fragment",result.fragment)
```

## request.Request类：

```py
from urllib import request
from urllib import parse

url = "需要爬取的地址链接"
headers = {"user Agent":"浏览器的user Agent"           #根据浏览器审查的信息加入模仿人为操作

           "Referer":"浏览器的Referer"           #根据浏览器审查的信息加入模仿人为操作

           }
data = {
        "first" : "true",           #根据浏览器审查的信息加入模仿人为操作
        "pn" : 1,           #根据浏览器审查的信息加入模仿人为操作
        "kd" : "Python"           #根据浏览器审查的信息加入模仿人为操作

        }
 request = request.Request(url,headers = headers,data = parse.urlencode(data).encode("utf-8"),method = "POST")
 resp = parse.urlencode(request)           # data = parse.urlencode(data).encode("utf-8") 通过parse.urlencode将data数据转码成浏览器可识别状态并用encode("utf-8")将转码后的记过变成bytes字节。method = "POST"表示请求方式是post方式。

 print(resp.read().decode("utf-8"))
```

## **ProxyHandler处理器\(代理\):**

```py
from urlli import request

url = "爬取的链接"    #确定爬取的链接，测试代理ip或本地ip有效性可用:“http:httpbin.org/ip”

Handler = request.ProxyHandler({"http":"IP:port"})        #使用ProxyHandlerr传入代理构建一个Handler
opener = request.build_opener(Handler)        #使用创建了的Handler构建一个opener
resp = opener.open(url)        #使用opener发送一个请求
print =(resp.read())
```



