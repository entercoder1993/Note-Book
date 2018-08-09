# Python网络爬虫与信息提取

* 文本工具类IDE

  * IDLE — 自带、默认、常用（适用于Python入门）
  * Sublime Text — 第三方专用编程工具

* 集成工具类IDE

  * PyCharm
  * Anaconda & Spyder

  

## Requests库入门

### Request库的安装

终端运行下列命令

```bash
$ pip install requests
```

获得源码

```bash
$ git clone git://github.com/kennethreitz/requests.git
```

也可以下载tarball

```
$ curl -OL https://github.com/requests/requests/tarball/master
```

现在完成后，使用如下命令进行安装

```bash
$ cd requests
$ pip install .
```

简单使用

```python
import requests
r = requests.get("http://www.baidu.com")
print(r.status_code) # 200
r.encoding = 'utf-8'
print(r.text) # baidu的html源码
```



### Requests库的7个主要方法

| 方法                | 说明                                           |
| ------------------- | ---------------------------------------------- |
| requests.requests() | 构造一个请求，支撑一下各方法的基础方法         |
| requests.get()      | 获取HTML网页的主要方法，对应于HTTP的GET        |
| requests.head()     | 获取HTML网页头信息的方法，对应于HTTP的HEAD     |
| requests.post()     | 向HTML网页提交POST请求的方法，对应于HTTP的POST |
| requests.put()      | 向HTML网页提交PUT请求的方法，对应与HTTP的PUT   |
| requests.patch()    | 向HTML网页提交局部修改请求，对应于HTTP的PATCH  |
| requests.delete()   | 向HTML页面提交删除请求，对应于HTTP的DELETE     |

#### Requests库的get()

![屏幕快照 2018-06-30 上午12.06.26](https://ws4.sinaimg.cn/large/006tKfTcgy1fsshyc4nm3j30g106vtdz.jpg)

* 使用方法

  ```python
  requests.get(url,params=None,**kwargs)
  ```

  * url：拟获取页面的url链接
  * params：url中的额外参数，字典或字节流格式，可选
  * **kwargs：12个控制访问的参数

* Response对象的属性

  | 属性                | 说明                                             |
  | ------------------- | ------------------------------------------------ |
  | r.status_code       | HTTP请求的返回状态，200表示连接成功，404表示失败 |
  | r.text              | HTTP相应内容的字符串形式，即，url对应的页面内容  |
  | r.encoding          | 从HTTP header中猜测的相应内容编码方式            |
  | r.apparent_encoding | 从内容中分析出的相应内容编码方式（备选编码方式） |
  | r.content           | HTTP相应内容的二进制形式                         |

  ![image-20180630001738309](https://ws1.sinaimg.cn/large/006tKfTcgy1fssi9kew65j30bv068wf1.jpg)

栗子：

```python
>>> import requests
>>> r = requests.get('https://www.baidu.com')
>>> r.encoding = 'utf-8'
>>> r.text
'<!DOCTYPE html>\r\n<!--STATUS OK-->
<html> 
	<head>
    ......
    </head>
    <body>
    ......
    </body> 
</html>
```

> r.encoding：如果header中不存在charset，则认为编码为ISO-8859-1

* Requests库的异常

  | 异常                      | 说明                                        |
  | ------------------------- | ------------------------------------------- |
  | requests.ConnectionError  | 网络连接错误异常，如DNS查询失败、拒绝连接等 |
  | requests.HTTPError        | HTTP错误异常                                |
  | requests.URLRequired      | URL缺失异常                                 |
  | requests.TooManyRedirects | 超过最大重定向次数，产生重定向异常          |
  | requests.ConnectTimeout   | 连接远程服务器超时异常                      |
  | requests.Timeout          | 请求URL超时，产生超时异常                   |

* 状态响应码status_code

  ```python
  >>> r = requests.get('https://www.baidu.com')
  >>> r.status_code
  200
  # 为方便引用，Requests还有一个内置的状态码查询对象
  >>> r.status_code == requests.codes.ok
  True
  # 如果是一个错误请求，可以通过Response.raise_for_status()来抛出异常
  >>> bad_r = requests.get('http://httpbin.org/status/404')
  >>> bad_r.status_code
  404
  
  >>> bad_r.raise_for_status()
  Traceback (most recent call last):
    File "requests/models.py", line 832, in raise_for_status
      raise http_error
  requests.exceptions.HTTPError: 404 Client Error
  # r.status == 200,当我们调用raise_for_status()时，得到的是
  >>> r.raise_for_status()
  None
  ```

* 爬取网页的通用代码框架TTP

  ```python
  import requests
  
  def getHTMLText(url):
      try:
          r = requests.get(url,time=30)
          r.raise_for_status() #如果状态不是200，将引发HTTPError异常
          r.encoding = r.apparent_encoding
          return r.text
      except：
      	return "产生异常"
      
  if __name__ = "__main__":
      url = 'https://www.baidu.com'
      print(getHTMLText(url))
  ```
  

### HTTP协议

  * HTTP，Hypertext Transfer Protocol，超文本传输协议。

  * HTTP是一个基于“请求与响应”模式的、装状态的应用层协议。

  * HTTP协议采用URL作为定位网络资源的标识

  * URL格式 `http://host[:port][path]` 
    * host：合法的Internet主机域名或IP地址
    * port：端口号，缺省端口为80
    * path：请求资源的路径

  * HTTP协议对资源的操作

    | 方法   | 说明                                                      |
    | ------ | --------------------------------------------------------- |
    | GET    | 请求获取URL位置的资源                                     |
    | HEAD   | 请求获取URL位置资源的响应消息报告，即获得该资源的头部信息 |
    | POST   | 请求向URL位置的资源后附加新的数据                         |
    | PUT    | 请求向URL位置存储一个资源，覆盖原URL位置的资源            |
    | PATCH  | 请求局部更新URL位置的资源，即改变该处资源的部分内容       |
    | DELETE | 请求删除URL位置存储的资源                                 |

    ![image-20180701153345007](https://ws4.sinaimg.cn/large/006tNc79gy1fsued0uqbtj30l005dn17.jpg)

  * 理解PATCH和PUT的区别

    * 采用PATCHA，仅向URL提交局部更新的请求
    * 采用PUT，必须将所有字段一并提交到URL，未提交字段被删除

  * Requests库的head()方法

    * ```python
      >>> r = requests.head('http://www.baidu.com')
      >>> r.headers
      {'Cache-Control': 'private, no-cache, no-store, proxy-revalidate, no-transform', 'Connection': 'Keep-Alive', 'Content-Encoding': 'gzip', 'Content-Type': 'text/html', 'Date': 'Sun, 01 Jul 2018 07:38:20 GMT', 'Last-Modified': 'Mon, 13 Jun 2016 02:50:26 GMT', 'Pragma': 'no-cache', 'Server': 'bfe/1.0.8.18'}
      >>> r.text
      ''
      ```

  * Requests库的post()方法

    ```python
    >>> payload = {'key1':'value1','key2':'value2'}
    >>> r = requests.post('http://www.baidu.com/post',data = payload)
    >>> print(r.text)
    { # 向URL POST一个字典，自动编码为form(表单)
        ...
        "form":{
            "key2":"value2",
            "key1":"value2"
        },
        ...
    }
    ```

  * Requests库的put()方法

    ```python
    >>> payload = {'key1':'value1','key2':'value2'}
    >>> r = requests.put("http://www.baidu.com/put',data = payload")
    >>> print(r.text)
    <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
    	<html>
        	<head>
    			<title>405 Method Not Allowed</title>
    		</head>
            <body>
    			<h1>Method Not Allowed</h1>
    			<p>The requested method PUT is not allowed for the URL 					/put',data=payload.</p>
    		</body>
    	</html>
    ```

    

### Requests库主要方法解析

* requests.request(method,url,**kwargs)

  * method：请求方式，对应get/put/post等7种

    * r = requests.request('GET',url,*kwargs)
    * r = requests.request('HEAD',url,*kwargs)
    * r = requests.request('POST',url,*kwargs)
    * r = requests.request('PUT',url,*kwargs)
    * r = requests.request('PATCH',url,*kwargs)
    * r = requests.request('delete',url,*kwargs)
    * r = requests.request('OPTIONS',url,*kwargs)

  * url：获取页面的url链接

  * **kwargs：控制访问参数，共13个

    * params：字典或字节序列，作为参数增加到url种

      ```python
      >>> kv = {'key1':'value1','key2':'value2'}
      >>> r = requests.request('GET','http://www.baidu.com/s',params=kv)
      >>> print(r.url)
      http://www.baidu.com/s?key1=value1&key2=value2
      ```

    * data：字典、字节序列或文件对象，作为Request的内容，向服务器提交资源时使用

      ```python
      >>> kv = {'key1':'value1','key2':'value2'}
      >>> r = requests.request('POST','http://www.baidu.com/s',data=kv)
      >>> body = '主体内容'
      >>> r = requests.request('POST','http://www.baidu.com/s',data=body)
      ```

    * json：JSON格式的数据，作为Request的内容

      ```python
      >>> kv = {'key1':'value1'}
      >>> r = requests.request('POST','http://www.baidu.com/s',json=kv)
      ```

    * headers：字典，HTTP定制头

      ```python
      >>> hd = {'user-agent':'Chrome/10'}
      >>> r = requests.request('POST','http://python123.io/ws',headers=hd)
      ```

    * cookies：字典或CookieJar，Request中的cookie

    * auth：元组，支持HTTP认证功能

    * file：字典类型，传输文件

      ```python
      >>> fs = {'file':open('data.xls','rb')}
      >>> r = requests.request('POST','http://python123.io/ws',files=fs)
      ```

    * timeout：设定超时时间，秒为单位

      ```python
      >>> r = requests.request('GET','http://www.baidu.com',timeout=10)
      ```

    * proxies：字典类型，设定访问代理服务器，可以增加登录认证

      ```python
      >>> pxs = {'http':'http://user:pass@10.10.10.1:1234','https':'https://10.10.10.1:4321'}
      >>> r = requests.request('GET','http://www.baidu.com',proxies=pxs)
      ```

    * allow_redirects：True/False，默认为True，重定向开关

    * stream：True/False，默认为True，获取内容立即下载开关

    * verify：True/False，默认为True，认证SSL证书开关

    * cert：本地SSL证书路径

## 网络爬虫的盗亦有道

* 网络爬虫的尺寸

![img](https://ws2.sinaimg.cn/large/006tNc79gy1fsuhzdxon1j30oz07s0u3.jpg)

* 网络爬虫的法律风险

  * 服务器上的数据有产权归属
  * 网络爬虫获取数据后牟利将带来法律风险

* 网络爬虫泄露数据

* 网络爬虫的限制

  * 来源审查：判断User-Agent进行限制
    * 检查来访HTTP协议头的User-Agent域，只响应浏览器或友好爬虫的访问
  * 发布公告：Robots协议
    * 告知所有爬虫网站的爬取策略，要求爬虫遵守

* Robots协议（Robots Exclusion Standard 网络爬虫排除标准）

  * 作用：网站告知网络爬虫哪些页面可以抓取，哪些不行 

  * 形式：在网站根目录下的robots.txt文件

  * https://www.jd.com/rboots.txt

    ```txt
    User-agent: * 
    Disallow: /?* 
    Disallow: /pop/*.html 
    Disallow: /pinpai/*.html?* 
    User-agent: EtaoSpider 
    Disallow: / 
    User-agent: HuihuiSpider 
    Disallow: / 
    User-agent: GwdangSpider 
    Disallow: / 
    User-agent: WochachaSpider 
    Disallow: /
    # 注释 * 代表所有 /代表根目录
    User-agent: *
    Disallow: /
    ```

  * 遵守方式

    * 网络爬虫：自动或人工识别robots.txt，再进行内容爬取
    * 约束性：Robots协议是建议但非约束性，网络爬虫可以不遵守，但存在法律风险

  * 理解

    ![img](https://ws2.sinaimg.cn/large/006tNc79gy1fsuinx4kc6j30np05wgmm.jpg)




## Requests库爬取实例

### 实例1：京东商品页面的爬取

```python
import requests
url = 'https://item.jd.com/2967929.html'
try:
    r = requests.get(url)
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.text[:1000])
except:
    print('爬取失败')
```

### 实例2：亚马逊商品的爬取

```python
import requests
url = "https://www.amazon.cn/dp/B00QJDOLIO/ref=lp_1536596071_1_1?s=amazon-devices&ie=UTF8&qid=1530439999&sr=1-1"
try:
    kv = {'user-agent':'Mozilla/5.0'}
    r = requests.get(url,headers=kv)
    r.raise_for_status()
    r.encoding = r.apparent_coding
    print(r.text[1000:2000])
except:
    print("爬取失败")
```

### 实例3：百度和360搜索关键字提交

* 百度

```python
import requests
keyword = "Python"
try:
    kv = {'wd':keyword}
    r = requests.get("http://www.baidu.com/s",params=kv)
    print(r.request.url)
    r.raise_for_status()
    print(len(r.text))
except:
    print("爬取失败")
```

* 360

```python
import requests
keyword = "Python"
try:
    kv = {'q':keyword}
    r = requests.get("http://www.so.com/s",params=kv)
    print(r.request.url)
    r.raise_for_status()
    print(len(r.text))
except:
    print("爬取失败")
```

### 实例4：网络图片的爬取和存储

```python
import requests
import os
root = "/Users/entercoder/Documents/123.jpg"
url = "https://ws2.sinaimg.cn/large/006tNc79gy1fsuinx4kc6j30np05wgmm.jpg"
path = root + url.split('/')[-1]
try:
    if not os.path.exists(root):
        os.mkdir(root)
    if not os.path.exists(path):
        r = requests.get(url)
        with open(path,'wb') as f:
            f.write(r.content)
            f.close()
            print("save successful")
    else:
        print("file already exists")
except:
    print("download fail")
```

### 实例5：IP地址归属地自动查询

```python
import requests
url = "http://ip138.com/ips138.asp?ip="
try:
    r = requests.get(url + '202.204.80.112')
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.text[-500:])
except:
    print("爬取失败")
```



## BeautifulSoup入门

### BeautifulSoup库的安装

* 使用pip安装

  ```bash
  $ pip3 install BeautifulSoup4
  ```

* 源码安装

  * [下载源码](http://www.crummy.com/software/BeautifulSoup/download/4.x/)

  * 通过setup.py安装

    ```bash
    $ Python setup.py install
    ```

* 安装解析器

  * lxml

    ```bash
    $ pip3 install lxml
    ```

  * html5lib

    ```bash
    $ pip3 install html5lib
    ```

* 主要解析器及使用方法

  | 解析器           | 使用方法                                                     |
  | ---------------- | ------------------------------------------------------------ |
  | Python标准库     | BeautifulSoup(markup,"html.parser")                          |
  | lxml HTML 解析器 | BeautifulSoup(markup,"lxml")                                 |
  | lxml XML 解析器  | BeautifulSoup(markup,["lxml-xml"])<br />BeautifulSoup(markup,"xml") |
  | html5lib         | BeautifulSoup(markup,"html5lib")                             |

* 测试

  ```python
  >>> import requests
  >>> r = requests.get('https://python123.io/ws/demo.html')
  >>> demo = r.text
  >>> from bs4 import BeautifulSoup
  >>> soup = BeautifulSoup(demo,'html.parser') # 需要解析的html格式的内容和解析器
  >>> print(soup.prettify())
  <html>
   <head>
    <title>
     This is a python demo page
    </title>
   </head>
   <body>
    <p class="title">
     <b>
      The demo python introduces several python courses.
     </b>
    </p>
    <p class="course">
     Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:
     <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">
      Basic Python
     </a>
     and
     <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">
      Advanced Python
     </a>
     .
    </p>
   </body>
  </html>
  ```

### BeautifulSoup库的基本元素

* BeautifulSoup库是解析、遍历、维护“标签树”的功能库

* BeautifulSoup类的基本元素

  | 基本元素        | 说明                                                       |
  | --------------- | ---------------------------------------------------------- |
  | Tag             | 标签，最基本的信息组织单元，分别用<>和</>标明开头和结尾    |
  | Name            | 标签的名字，\<p>...\<p>的名字是'p'，格式：\<tag>.name      |
  | Attributes      | 标签的属性，字典形式组织，格式：\<tag>.attrs               |
  | NavigableString | 标签内非属性字符串，\<>...</>中字符串，格式：\<tag>.string |
  | Comment         | 标签内字符串的注释部分，一种特殊的Comment类型              |

  ![img](https://ws4.sinaimg.cn/large/006tNc79gy1fsuqg0h7bvj30nb09d3zm.jpg)

  ```python
  >>> import requests
  >>> from bs4 import BeautifulSoup
  
  >>> r = requests.get("http://python123.io/ws/demo.html")
  >>> demo = r.text
  >>> soup = BeautifulSoup(demo,"html.parser")
  >>> soup.title
  <title>This is a python demo page</title>
  >>> tag = soup.a
  >>> tag
  <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a>
  >>> soup.a.name
  'a'
  >>> soup.a.parent.name
  'p'
  >>> soup.a.parent.parent.name
  'body'
  >>> tag.attrs
  {'href': 'http://www.icourse163.org/course/BIT-268001', 'class': ['py1'], 'id': 'link1'}
  >>> tag.attrs['class']
  ['py1']
  >>> tag.attrs['href']
  'http://www.icourse163.org/course/BIT-268001'
  >>> type(tag.attrs)
  <class 'dict'>
  >>> type(tag)
  <class 'bs4.element.Tag'>
  >>> soup.a.string
  'Basic Python'
  >>> soup.p.string
  'The demo python introduces several python courses.'
  >>> type(soup.p.string)
  <class 'bs4.element.NavigableString'>
  >>> newsoup = BeautifulSoup("<b><!-- This is a comment --></b><p>This is not a comment</p>","html.parser")
  # 不常用
  >>> newsoup.b.string
  ' This is a comment '
  >>> type(newsoup.b.string)
  <class 'bs4.element.Comment'>
  >>> newsoup.p.string
  'This is not a comment'
  >>> type(newsoup.p.string)
  <class 'bs4.element.NavigableString'>
  ```

  

### 基于bs4库的HTML内容遍历方法

* 遍历方式

  ![img](https://ws4.sinaimg.cn/large/006tNc79gy1fsuqjfmvegj30no08ojse.jpg)

  * 标签树的下行遍历

    | 属性         | 说明                                                    |
    | ------------ | ------------------------------------------------------- |
    | .contents    | 子节点的列表，将所有\<tag>所有儿子节点存入列表          |
    | .children    | 子节点的迭代类型，与.contents类似，用于循环遍历儿子节点 |
    | .descendants | 子孙节点的迭代类型，包含所有子孙节点，用于循环遍历      |

    ```python
    >>> from bs4 import BeautifulSoup
    >>> soup = BeautifulSoup(demo,"html.parser")
    >>> soup.head
    <head><title>This is a python demo page</title></head>
    >>> soup.head.contents
    [<title>This is a python demo page</title>]
    >>> soup.body.contents
    ['\n', <p class="title"><b>The demo python introduces several python courses.</b></p>, '\n', <p class="course">Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:
    <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a> and <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>.</p>, '\n']
    >>> len(soup.body.contents)
    5
    >>> soup.body.contents[1]
    <p class="title"><b>The demo python introduces several python courses.</b></p>
    >>> 
    # 遍历儿子节点
    for child in soup.body.children:
        print(child)
    # 遍历子孙节点
    for child in soup.body.descendants:
        print(children)
    ```

  * 标签树的上行遍历

    | 属性     | 说明                                           |
    | -------- | ---------------------------------------------- |
    | .parent  | 节点的父亲标签                                 |
    | .parents | 节点的先辈标签的迭代烈性，用于循环遍历先辈节点 |

    ```python
    >>> soup = BeautifulSoup(demo,"html.parser")
    >>> soup.title.parent
    <head><title>This is a python demo page</title></head>
    >>> soup.html.parent
    <html><head><title>This is a python demo page</title></head>
    <body>
    <p class="title"><b>The demo python introduces several python courses.</b></p>
    <p class="course">Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:
    <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a> and <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>.</p>
    </body></html>
    >>> soup.parent
    # 标签树的上行遍历
    >>> soup = BeautifulSoup(demo,"html.parser")
    >>> for parent in soup.a.parents:
        	if parent is None:
                print(parent)
            else:
                print(parent.name)
    ```

  * 标签树的平行遍历

    | 属性               | 说明                                                 |
    | ------------------ | ---------------------------------------------------- |
    | .next_sibling      | 返回按照HTML文本顺序的下一个平行节点标签             |
    | .previous_sibling  | 返回按照HTML文本顺序的上一个平行节点标签             |
    | .next_siblings     | 迭代类型，返回按照HTML文本顺序的后续所有平行节点标签 |
    | .previous_siblings | 迭代类型，返回按照HTML文本顺序的前续所有平行节点标签 |

    ```python
    >>> soup = BeautifulSoup(demo,"html.parser")
    >>> soup.a.next_sibling
    ' and '
    >>> soup.a.next_sibling.next_sibling
    <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>
    >>> soup.a.previous_sibling
    'Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:\r\n'
    >>> soup.a.previous_sibling.previous_sibling
    
    # 标签树的平行遍历
    # 遍历后续节点
    for sibling in soup.a.next_siblings
    	print(sibling)
    # 遍历前续节点
    for sibling in soup.a.previous_siblings:
        print(sibling)
    ```

  * 总结

    ![img](https://ws3.sinaimg.cn/large/006tNc79gy1fsurizrbltj30ns0bfgne.jpg)

### 基于bs4库的HTML格式输出

* prettify()方法可以格式化输出HTML文本

  ```python
  >>> soup = BeautifulSoup(demo,"html.parser")
  >>> soup.prettify()
  >>> print(soup.prettify())
  ```

## 信息标记的三种形式

* 三种形式

  * XML -- eXtensible Markup Language
  * JSON -- JavaScript Object Notation
  * YAML -- 

* 三种信息标记形式的比较

* 信息提取的一般方法

* 基于bs4库的HTML内容查找方法

  * <>.find_all(name,attrs,recursive,string,**kwargs) 返回一个列表类型，存储查找结果

    * name：对标签名称的检索字符串

      ```python
      >>> soup.find_all('a')
      [<a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a>, <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>]
      >>> soup.find_all(['a','b'])
      [<b>The demo python introduces several python courses.</b>, <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a>, <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>]
      >>> for tag in soup.find_all(True):
      	print(tag.name)
      html
      head
      title
      body
      p
      b
      p
      a
      a
      >>> import re
      >>> for tag in soup.find_all(re.compile('b')):
      	print(tag.name)
      body
      b
      ```

    * attrs：对标签属性值的检索字符窜，可标注属性检索

    * recursive：是否对子孙全部检索，默认True

    * string：\<>...\</>中字符串区域的检索字符串

  * \<tag>(...)等价于\<tag>.find_all(...) 

  * soup(...)等价于soup.find_all(...)

  * 七个常用扩展方法

    | 方法                        | 说明                                                    |
    | --------------------------- | ------------------------------------------------------- |
    | <>.find()                   | 搜索且只返回一个结果，字符串类型，同.find_all()参数     |
    | <>.find_parents()           | 在先辈节点中搜索，返回列表类型，同.find_all参数         |
    | <>.find_parent()            | 在先辈节点中返回一个结果，字符串类型，同.find()参数     |
    | <>.find_next_siblings()     | 在后续平行节点中搜索，返回列表类型，同.find_all()参数   |
    | <>.find_next_sibling()      | 在后续平行节点中返回一个结果，字符串类型，同.find()参数 |
    | <>.find_previous_siblings() | 在前续平行节点中搜索，返回列表类型，同.find_all()参数   |
    | <>.find_previous_sibling()  | 在前续平行节点中返回一个结果，字符串类型，同.find()参数 |

### 实例1：中国大学排名定向爬虫

* 功能描述

  * 输入：大学排名URL连接
  * 输出：大学排名信息的屏幕输出（排名，大学名称，总分）
  * 技术路线：**requests-bs4**
  * 定向爬去：仅对输入URL进行爬取，不扩展爬取

* 程序的结构设计

  1. 从网络上获取大学排名网页内容 -- getHTMLText()
  2. 提取网页内容中信息到合适的数据结构 -- fillUnivList()
  3. 利用数据结构展示并输出结果 -- fillUnivList()

* 代码

  ```python
  import requests
  from bs4 import BeautifulSoup
  import bs4
  
  def getHTMLText(url):
      try:
          r = requests.get(url, timeout=30)
          r.raise_for_status()
          r.encoding = r.apparent_encoding
          return r.text
      except:
          return "except"
  
  def fillUnivList(ulist, html):
      soup = BeautifulSoup(html, 'html.parser')
      for tr in soup.find('tbody').children:
          if isinstance(tr,bs4.element.Tag):
              tds = tr('td')
              ulist.append([tds[0].string, tds[1].string, tds[3].string])
  
  def printUnivList(ulist, num):
      tplt = "{0:^10}\t{1:{3}^10}\t{2:^10}"
      print(tplt.format("排名", "学校", "分数",chr(12288)))
      for i in range(num):
          u = ulist[i]
          print(tplt.format(u[0], u[1], u[2],chr(12288)))
  
  if __name__ == '__main__':
      uinfo = []
      url = 'http://zuihaodaxue.com/zuihaodaxuepaiming2018.html'
      html = getHTMLText(url)
      fillUnivList(uinfo, html)
      printUnivList(uinfo, 100)
  
  ```

## 正则表达式

正则表达式是用来简洁表达一组字符串的表达式。

* 编译：将符合正则表达式语法的字符串转换成正则表达式特征

* 语法

  | 操作符 | 说明                             | 实例                                    |
  | ------ | -------------------------------- | --------------------------------------- |
  | .      | 表示任何单个字符                 |                                         |
  | []     | 字符集，对单个字符给出取值范围   | [abc]表示a、b、c，[a-z]表示a到z单个字符 |
  | [^]    | 非字符集，对单个字符给出排除范围 | [^abc]表示非a或b或c的单个字符           |
  | *      | 前一个字符0次或无限次扩展        | abc*表示ab、abc、abcc、abccc等          |
  | +      | 前一个字符1次或无限次扩展        | abc+表示abc、abcc、abccc等              |
  | ?      | 前一个字符0次或1次扩展           | abc?表示ab、abc                         |
  | \|     | 左右表达式任意一个               | abc\|def表示abc、def                    |
  | {m}    | 扩展前一个字符m次                | ab{2}c表示abbc                          |
  | {m,n}  | 扩展前一个字符m至n次（含n）      | ab{1,2}表示abc、abbc                    |
  | ^      | 匹配字符串开头                   | ^abc表示abc且在一个字符串的开头         |
  | $      | 匹配字符串结尾                   | abc&表示abc且在一个字符串的结尾         |
  | \d     | 数字，等价于[0-9]                |                                         |
  | \w     | 单词字符，等价于[A-Za-z0-9_]     |                                         |
  | ()     | 分组标记，内部只能使用\|操作符   | (abc)表示abc，(abc\|def)表示abc、def    |

### Re库的基本使用

Re库是Python的标准库，主要用于字符串匹配，调用方式：import re

* 正则表达式的表示类型

  * raw string类型（原生字符串类型）
  * string类型

* Re库主要功能函数

  | 函数          | 说明                                                         |
  | ------------- | ------------------------------------------------------------ |
  | re.search()   | 在一个字符串中搜索匹配正则表达式的第一个位置，返回match对象  |
  | re.match()    | 在一个字符串的开始位置起匹配正则表达式，返回match对象        |
  | re.findall()  | 搜索字符串，以列表类型返回全部能匹配的子串                   |
  | re.split()    | 将一个字符串按照正则表达式匹配结果进行分割，返回列表类型     |
  | re.finditer() | 搜索字符串，返回一个匹配结果的迭代类型，每隔迭代元素是match对象 |
  | re.sub()      | 在一个字符串中替换所有匹配正则表达式的子串，返回替换后的字符串 |

  * re.search(pattern,string,flags=0)
    * pattern：正则表达式的字符串或原生字符串表示

    * string：待匹配字符串

    * flags：正则表达式使用时的控制标记

      | 常用标记                 | 说明                                                         |
      | ------------------------ | ------------------------------------------------------------ |
      | re.I   re.IGNORECASE     | 忽略正则表达式的大小写，[A-Z]能后匹配小写字符                |
      | re.M    re.MULTILINE     | 正则表达式中的^操作符能够将给定字符串的每行当做匹配开始      |
      | re.S           re.DOTALL | 正则表达式中的.操作符能够匹配所有字符，默认匹配除换行外的所有字符 |

      ```python
      >>> import re
      >>> match = re.search(r'[1-9]\d{5}','bit 100081')
      >>> if match:
      	print(match.group(0))
      
      100081
      ```

  * re.match(pattern,string,flags=0)

    * pattern：正则表达式的字符串或原生字符串表示

    * string：待匹配字符串

    * flags：正则表达式使用时的控制标记

      ```python
      match = re.match(r'[1-9]\d{5}','100081 bit')
      ```

  * re.findall(pattern.string.flags=0)

    * pattern：正则表达式的字符串或原生字符串表示

    * string：待匹配字符串

    * flags：正则表达式使用时的控制标记

      ```python
      >>> ls = re.findall(r'[1-9]\d{5}','bit100081 tsu 100084')
      >>> ls
      ['100081', '100084']
      ```

  * re.split(pattern,string,maxsplit=0,flags=0)

    * pattern：正则表达式的字符串或原生字符串表示

    * string：待匹配字符串

    * maxsplit：最大分个数，剩余部分作为最后一个元素输出

    * flags：正则表达式使用时的控制标记

      ```python
      >>> ls = re.split(r'[1-9]\d{5}','bit100081 tsu100084',maxsplit=1)
      >>> ls
      ['bit', ' tsu100084']
      ```

  * re.finditer(pattern,string,flags=0)

    * pattern：正则表达式的字符串或原生字符串表示

    * string：待匹配字符串

    * flags：正则表达式使用时的控制标记

      ```python
      >>> for m in re.finditer(r'[1-9]\d{5}','bit100081 tsu100084'):
      	if m:
      		print(m.group(0))
      	
      100081
      100084
      ```

  * re.sub(pattern,repl,string,count=0,flags=0)

    * pattern：正则表达式的字符串或原生字符串表示

    * repl：替换匹配字符串的字符串

    * string：待匹配字符串

    * count：匹配的最大替换次数

    * flags：正则表达式使用时的控制标记

      ```python
      >>> re = re.sub(r'[123]','456','1237878712398798123',count=2)
      >>> re
      '45645637878712398798123'
      ```

* Re库的另一种等价用法

  * 函数式用法：一次性操作

    ```python
    >>> rst = re.search(r'[1-9]\d{5}','bit 100081')
    ```

  * 面向对象用法：编译后多次操作

    ```python
    >>> pat = re.compile(r'[1-9]\d{5}')
    >>> rst = pat.search('bit 100081')
    ```

* regex = re.compile(pattern,flags=0) -- 将正则表达式的字符串形式编译成正则表达式对象

  * regex.search()
  * regex.match()
  * regex.findall()
  * regex.split()
  * regex.finditer()
  * regex.sub()

* Re库的Match函数

  * Match对象的属性

    | 属性    | 说明                                  |
    | ------- | ------------------------------------- |
    | .string | 待匹配的文本                          |
    | .re     | 匹配时使用的pattern对象（正则表达式） |
    | .pos    | 正则表达式搜索文本的开始位置          |
    | .endpos | 正则表达式搜索文本的结束位置          |

  * Match对象的方法

    | 方法      | 说明                             |
    | --------- | -------------------------------- |
    | .group(0) | 获取匹配后的字符串               |
    | .start()  | 匹配字符串在原始字符串的开始位置 |
    | .end      | 匹配字符串在原始字符串的结束位置 |
    | .span     | 返回(.start(),.end())            |

* Re库的贪婪匹配和最小匹配

  * 贪婪匹配：Re库默认采用贪婪匹配，即输出匹配最长的子串

  * 最小匹配

    | 操作符 | 说明                                |
    | ------ | ----------------------------------- |
    | *?     | 前一个字符0次或无限次扩展，最小匹配 |
    | +?     | 前一个字符1次或无限次扩展，最小匹配 |
    | ??     | 前一个字符0次或1次扩展，最小匹配    |
    | {m,n}? | 扩展前一个字符m至n次(含n)，最小匹配 |

### 实例2 淘宝商品比价定向爬虫

* 功能描述

  * 目标：获取淘宝搜索页面的信息，提取其中的商品名称和价格
  * 理解：淘宝的搜索接口和翻页的处理
  * 技术路线：requests-re

* 程序的设计结构

  1. 提交商品搜索请求，循环获取页面
  2. 对于每个商品，提取商品名称和价格信息
  3. 将信息输出到屏幕上

* 代码实现

  ```python
  import requests
  import re
  
  def getHTMLText(url):
      try:
          r = requests.get(url)
          r.raise_for_status()
          r.encoding = r.apparent_encoding
          return r.text
      except:
          return ""
  
  def parsePage(ilt,html):
      try:
          plt = re.findall(r'"view_price":"[\d.]*"',html)
          tlt = re.findall(r'"raw_title":".*?"',html)
          for i in range(len(plt)):
              price = eval(plt[i].split(':')[1])
              title = eval(tlt[i].split(':')[1])
              ilt.append([price,title])
      except:
          print("")
  
  def printGoodsList(ilt):
      tplt = "{:4}\t{:8}\t{:16}"
      print(tplt.format("xuhao","jiage","shangpin name"))
      count = 0
      for g in ilt:
          count = count + 1
          print(tplt.format(count,g[0],g[1]))
      
  
  def main():
      goods = 'shubao'
      depth = 2
      start_url = 'https://s.taobao.com/search?q=%' + goods
      infoList = []
      for i in range(depth):
          try:
              url = start_url + '&s=' + str(44*i)
              html = getHTMLText(url)
              parsePage(infoList,html)
          except:
              continue
      printGoodsList(infoList)
  
  main()
  ```

### 实例3 股票数据定向爬虫

* 功能描述

  * 目标：获取上交所和深交所所有股票的名称和交易信息
  * 输出：保存到文件中
  * 技术路线：requests-bs4-re

* 程序结构设计

  1. 从东方财富网选取股票列表
  2. 根据股票列表逐个到百度股票获取个股信息
  3. 将结果存储到文件

* 代码实现

  ```python
  import requests
  from bs4 import BeautifulSoup
  import traceback
  import re
  
  def getHTMLText(url,code='utf-8'):
      try:
          r = requests.get(url)
          r.raise_for_status()
          r.encoding = code
          return r.text
      except:
          return ""
  
  def getStockList(lst, stockURL):
      html = getHTMLText(stockURL)
      soup = BeautifulSoup(html, 'html.parser')
      a = soup.find_all('a')
      for i in a:
          try:
              href = i.attrs['href']
              lst.append(re.findall(r"[s][hz]\d{6}", href)[0])
          except:
              continue
  
  def getStockInfo(lst, stockURL, fpath):
      count = 0
      for stock in lst:
          url = stockURL + stock + ".html"
          html = getHTMLText(url)
          try:
              if html == "":
                  continue
              infoDict = {}
              soup = BeautifulSoup(html, "html.parser")
              stockInfo = soup.find_all('div', attrs={'class': 'stock-bets'})[0]
  
              name = stockInfo.find(attrs={'class':'bets-name'})[0]
              infoDict.update({'stockname': name.text.split()[0]})
  
              keyList = stockInfo.find_all('dt')
              valueList = stockInfo.find_all('dd')
              for i in range(len(lst)):
                  # if i == 20:
                  #     break
                  key = keyList[i].text
                  val = valueList[i].text
                  infoDict[key] = val
  
              with open(fpath, 'a', encoding='utf-8') as f:
                  f.write(str(infoDict) + '\n')
                  count = count + 1
                  print('\r当前速度：{:.2f}%'.format(count*100/len(lst)), end='')
          except:
              count = count + 1
              print('\r当前速度：{:.2f}%'.format(count*100/len(lst)),end='')
              # traceback.print_exc()
              continue
  
  def main():
      stock_list_url = "http://quote.eastmoney.com/stocklist.html"
      stock_info_url = "https://gupiao.baidu.com/stock/"
      output_file = "/Users/entercoder/Documents/stock.txt"
      slist = []
      getStockList(slist, stock_list_url)
      getStockInfo(slist, stock_info_url, output_file)
  
  main()
  ```

  

​    

​    