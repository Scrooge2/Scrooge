## **urllib库：**

urlibl库是Python中的一个基本库，可以模拟浏览器的行为，并且url的所有网络请求方法都被集成到`urllib.request`模块下面

## urllib库的urlopen函数:

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

data = {"name":"爬虫数据","greet":"Hello World","age":10}        #data赋值的是一个数组需要用上大括号{}且数组中的元素需要使用""

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

result = parse.urlparse(url)        
#urlparse用法和urlsplit想法基本相同，urlparse可获取params属性，而urlsplit则获取不到。

#resul = parse.urlsplit(url)        
#urlparse用法和urlsplit想法基本相同，urlparse可获取params属性，而urlsplit则获取不到。

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

## **Cookie格式:**

```
Set-Cookie:NAME=VALUE:Expires:Max-age-DATE:Path=PATH:Domain:DOMAIN_NAME:SECURE
```

参数意义:

> **NAME : cookie的名字**
>
> **VALUE : cookie的值**
>
> **Expires : cookie的过期时间**
>
> **Path : cookie作用的路径**
>
> **Domain : cookie作用的域名**
>
> **SECURE : 是否只在https协议下起作用**

## 使用cookielib库和HTTPookieProcessr登录:

Cookie是指网站服务器为了辨别用户身份和进行Session跟踪而储存在用户浏览器上的文本文件，Cookie可以保持登录用户的信息到用户下次与服务器的对话。

示例代码如下:

```py
from urllib import request

Headers = {
                "User-Agent" : "input",               #这里的input是浏览器登录网站的User-Agent
                "Cookie" : "input"                #这里的input是访问网站的Cookie
}

url = "input"                #这里的input是访问的网站链接

req = reque.Request(url,Headers = Headers)                #
resp = request.urlopen(req)
with open("input.html","w") as fp:                #这里的input是保存的html文件的名字
    fp.write(resp.read().decode("utf-8"))
```



