# Python网络爬虫开发实战

## 一、开发环境配置

### 1.1 Python3

* 相关链接
  * 官方网站：https://www.python.org
  * 下载地址：https://www.python.org/downloads
  * 第三方库：https://pypi.org
  * 官方文档：https://docs.python.org/3 [中文文档](http://docspy3zh.readthedocs.io/en/latest/index.html)
  * 中文教程：
    * 菜鸟教程：http://www.runoob.com/python3/python3-tutorial.html
    * 廖雪峰Python3教程：[点击这里](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000)

### 1.2 请求库的安装

#### Request的安装

* 相关链接
  * GitHub：https://github.com/requests/requests
  * PyPI：https://pypi.org/project/requests/
  * 官方文档：http://docs.python-requests.org/en/master/
  * 中文文档：http://cn.python-requests.org/zh_CN/latest/

#### Selenium的安装

* 相关链接
  * 官方网站：https://www.seleniumhq.org/
  * GitHub：https://github.com/SeleniumHQ/Selenium
  * PyPI：https://pypi.org/project/selenium/
  * 官方文档：http://selenium-python.readthedocs.io/
  * 中文文档：http://selenium-python-zh.readthedocs.io

#### ChromeDriver的安装

* 相关链接
  * 官方地址：http://chromedriver.chromium.org/
  * 下载地址：https://chromedriver.storage.googleapis.com/index.html?path=2.40/（需根据Chrome的版本下载对应的ChromeDriver）
* 环境变量配置：
  * Windows：将chromedriver.exe文件拖到Python的Scripts目录下即可。
  * Linux和Mac下
    * 将文件移动到/usr/bin目录下`suod mv chromedriver /usr/bin`
    * 或者将ChromeDriver配置到$PATH`export PATH="$PATH:/usr/local/chromedriver"`

#### GeckoDriver的安装

* 相关链接
  * Github：https://github.com/mozilla/geckodriver
  * 下载地址：https://github.com/mozilla/geckodriver/releases

#### PhantomJS的安装

* 相关链接
  * 官方网站：http://phantomjs.org
  * 官方文档：http://phantomjs.org/quick-start.html
  * 下载地址：http://phantomjs.org/download.html
  * API接口说明：http://phantomjs.org/api/command-line.html

#### aiohttp的安装

* 相关链接
  * 官方文档：https://docs.aiohttp.org/en/stable/
  * GitHub：https://github.com/aio-libs/aiohttp
  * PyPI：https://pypi.org/project/aiohttp/

### 1.3 解析库的安装

#### lxml的安装

* 相关链接
  * 官方网站：https://lxml.de/
  * GitHub：https://github.com/lxml/lxml
  * PyPI：https://pypi.org/project/lxml/

#### Beautiful Soup4的安装

* 相关链接
  * 官方网站：https://www.crummy.com/software/BeautifulSoup/bs4/doc/
  * 中文文档：https://www.crummy.com/software/BeautifulSoup/bs4/doc.zh/
  * PyPI：https://pypi.org/project/beautifulsoup4/

#### pyquery的安装

- 相关链接
  - 官方网站：https://pythonhosted.org/pyquery/
  - GitHub：https://github.com/gawel/pyquery/
  - PyPI：https://pypi.org/project/pyquery/

#### tesserocr的安装

- 相关链接
  - tesserocr GitHub：https://github.com/tesseract-ocr/tesseract
  - tesserocr PyPI：https://pypi.org/project/tesserocr/
  - tesseract 下载地址：https://github.com/tesseract-ocr/tesseract/wiki
  - tesseract GitHub：https://github.com/tesseract-ocr/tesseract
  - tesseract语言包：https://github.com/tesseract-ocr/tessdata
  - tesseract文档：https://github.com/tesseract-ocr/tesseract/wiki/Documentation

### 1.4 数据库的安装

#### MySQL的安装

#### MongoDB的安装

#### Redis的安装

### 1.5 存储库的安装

#### PyMySQL的安装

#### PyMongo的安装

#### redis-py的安装

#### RedisDump的安装

### 1.6 Web库的安装

#### Flask的安装

#### Tornado的安装

### 1.7 App爬取相关的库安装

#### Charles的安装

#### mitmproxy的安装

### 1.8 爬虫框架的安装

#### pyspider的安装

#### Scrapy的安装

#### Scrapy-Splash的安装

#### Scrapy-Redis的安装

### 1.9 部署库相关的库的安装

#### Docker的安装

#### Scrapyd的安装

#### Scrapyd-Client的安装

#### Scrapyd API的安装

#### Scrapyrt的安装

#### Gerapy的安装

## 二、爬虫基础

### 2.1 HTTP基本原理

> **请求**网站并**提取**数据的**自动化**程序

* URI和URL
  * URI全称Uniform Resource Identifier，即统一资源标志符

  * URL全称Universal Resource Locator，即统一资源定位符

  * URL是URI的子集

  *   另一个子类为URN全称Universal Resource Name，即统一资源名称

  *   关系

      ![img](https://ws2.sinaimg.cn/large/006tNc79gy1ft42wp69kxj308704c74c.jpg)

* 超文本(hypertext)，网页就是超文本解析而成的。

* HTTP和HTTPS

  *   HTTP全称Hyper Text Transfer Protocol，中文名称:超文本传输协议。是用于从网络传输文本数据到本地浏览器的传送协议，它能保证高效而准确地传送超文本文档。
  *   HTTPS全称Hyper Text Transfer Protocol voer Secure  Socket Layer，是以安全为目标的HTTP通道，即HTTP的安全版，HTTP下加入SSL层，简称HTTPS
      *   作用:
          *   建立一个信息安全通道来保证数据传输的安全
          *   确认网站的真实性，凡是使用了HTTPS的网站，都可以通过点击浏览地址栏的锁头标志来查看网站认证之后的真实信息，也可以通过CA机构颁发的安全签章来查询。

* HTTP请求过程

  1. 浏览器向网站所在的服务器发送一个请求
  2. 网站服务器接受到这个请求后进行处理和解析
  3. 返回对应的响应（响应包含页面的源代码等内容）
  4. 传回给浏览器（浏览器对其进行解析，便将网页呈现出来）

  ![img](https://ws2.sinaimg.cn/large/006tNc79ly1ft4s5tla9lj30c204o3yt.jpg)

  5. Chrome浏览器

     ![image-20180710151010965](https://ws2.sinaimg.cn/large/006tNc79ly1ft4s9daqiqj31hb0budj9.jpg)

     * Name：请求的名称，一般会将URL的最后一部分内容当做名称
     * Status：响应的状态码，200代表响应是正常的
     * Type：请求的文档类型
     * Initiator：请求源。用来标记请求是由哪个对象或进程发起的
     * Size：从服务器下载的文件和请求的资源大小。如果从缓存中取得的数据，则该列会像是from cache
     * Time：发起请求到获取响应所用的总时间
     * Waterfall：网络请求的可视化瀑布流

* 请求

  * 请求方法

    * GET
    * POST
    * 区别
      * GET请求中的参数包含在URL里面，数据可以在URL中看到，而POST请求的URL不会包含这些数据，数据都是通过表单形式传输的，会包含在请求体中
      * GET请求提交的数据最多只有1024字节，而POST方式没有限制
    * 其他方法：
      * GET、HEAD、POST、PUT、DELETE、OPTIONS、CONNECT、TRACE等

    | 方法    | 描述                                                         |
    | ------- | ------------------------------------------------------------ |
    | GET     | 请求页面，并返回页面内容                                     |
    | HEAD    | 类似于GET请求，只不过返回的响应中没有具体的内容，用于获取报头 |
    | POST    | 大多用于提交表单或上传文件，数据包含在请求体中               |
    | PUT     | 从客户端向服务器传送的数据取代指定文档中的内容               |
    | DELETE  | 请求服务器删除指定的页面                                     |
    | CONNECT | 把服务器当做跳板，让服务器代替客户端访问其他网页             |
    | OPTIONS | 允许客户端查看服务器的性能                                   |
    | TRACE   | 回显服务器收到的请求，主要用于测试或诊断                     |

  * 请求的网址：即统一资源定位符URL，它可以唯一确定我们想请求的资源

  * 请求头

    * Accept：请求报头域，用于指定客户端可接受哪些类型的信息
    * Accept-Language：制定客户端可接受的语言类型
    * Accept-Encoding：指定客户端可接受的内容编码
    * Host：用于请求资源的主机IP和端口号，其内容为请求URL的原始服务器或网关的位置
    * Cookie：常用复数形式Cookies，这是网站为了辨别用户进行会话跟踪而存储在用户本地的数据。主要功能是维持当前访问会话。
    * Referer：便是请求是从哪个页面发过来的，服务器可以拿到这一信息并做相应的处理，如做来源统计、防盗链处理等。
    * User-Agent：简称UA，它是一个特殊的字符串头，可以使服务器识别客户使用的操作系统及版本、浏览器及版本等信息。在做爬虫时加上此信息，可以伪装为浏览器；如果不加，很可能会被识别为爬虫。
    * Content-Type：也叫互联网媒体类型或者MIME类型，如HTTP协议消息头中，它用来表示具体请求中的媒体类型信息。text\html代表HTML格式，image/gif代表GIF图片，application/json代表JSON类型等。

  * 请求体：登录之前，填写的用户名和密码信息，提交时这些内容就会以表单数据的形式提交给服务器，只有有设置Request Headers中的Content-Type为application/x-www-form-urlencoded时，才会以表单数据的形式提交。

    | Content-Type                      | 提交数据的方式 |
    | --------------------------------- | -------------- |
    | application/x-www-form-urlencoded | 表单数据       |
    | mulitipart/form-data              | 表单文件上传   |
    | application/json                  | 序列化JSON数据 |
    | text/xml                          | XML数据        |

* 响应

  * 响应状态码（Response Status Code）

    ![img](https://ws2.sinaimg.cn/large/006tKfTcgy1ft6aro73clj30is0o4wix.jpg)

    ![img](https://ws4.sinaimg.cn/large/006tKfTcgy1ft6arvf6lcj30in03q74u.jpg)

  * 响应头（Response Headers）

    * Date：标识响应产生的时间
    * Last-Moidfied：指定资源的最后修改时间
    * Content-Encoding：指定响应内容的编码
    * Server：包含服务器的信息，比如名称、版本号等
    * Content-Type：文档类型，指定返回的数据类型是什么就返回什么类型
    * Set-Cookie：设置Cookies。响应头中的Set-Cookie告诉浏览器需要将此内容放在Cooikes中，下次请求携带Cookies请求
    * Expires：指定响应的过期时间，可以使代理服务器或浏览器将加载的内容更新到缓存中。如再次访问时，就可以直接从缓存中加载。

  * 响应体（Response Body）：响应的正文数据都在响应体重，比如请求网页时，它的响应就是网页的HTML代码。爬虫请求网页后，要解析的内容就是响应体。

    

### 2.2 网页基础

* 网页可以分成三大部分：HTML、CSS和JavaScript

  * HTML（Hyper Text Markup Language，即超文本标记语言）：是用来描述网页的一种协议
  * CSS（Cascading Sytle Sheet，即层叠样式表）：“层叠”是指当在HTML中引用了数个样式文件，并且样式发生冲突时，浏览器能依据层叠顺序处理。“样式”指网页中文字大小、颜色、元素间距、排列等格式
  * JavaScript：简称JS，是一种脚本语言。HTML和CSS配合使用，提供给用户的只是一种静态信息，缺乏交互性。网页里的交互和动画效果，通常都是JavaScript的功劳。它的出现使得用户与信息之间不只是一种浏览与显示的关系，而是实现了一种实时、动态、交互的页面功能。

* 网页的结构

  ```html
  <!-- 定义文档类型 -->
  <!DOCTYPE HTML>
  <html>
      <!-- head标签内定义了一些页面的配置和引用 -->
      <head>
          <!-- 指定网页编码为utf-8 -->
          <meta charset="utf-8">
          <!-- 网页的标题 -->
          <title>This is a Demo</title>
      </head>
      <body>
          <!-- div标签定义了网页中的区块，id是container，id的内容在网页中是唯一的 -->
          <div id="container">
              <!-- class所谓wrapper -->
          	<div class="wrapper">
                  <h2>
                      Hello World
                  </h2>
                  <p>
                      Hello,This iis a paragraph.
                  </p>
              </div>    
          </div>
      </body>
  </html>
  ```

* 节点树及节点间的关系：在HTML中，所有标签定义的内容都是节点，它们构成了HTML DOM树

  > DOM(Document Object Model)文档对象模型。它定义了访问HTML和XML文档的标准

  * W3C DOM标准被分为3个不同的部分

    1. 核心DOM：针对任何结构化文档的标准模型
    2. XML DOM：针对XML文档的标准模型
    3. HTML DOM：针对HTML文档的标准模型

  * 根据W3C的HTML DOM标准，HTML文档中的所有内容都是节点

    * 整个文档是一个文档节点
    * 每个HTML元素是元素节点
    * HTML元素内的文本是文本节点
    * 每个HTML属性都是属性节点
    * 注释是注释节点

  * 节点树

    ![img](https://ws1.sinaimg.cn/large/006tKfTcly1ftnbc6u3r1j30di078mxt.jpg)

  * 节点树及节点之间的关系

    ![img](https://ws3.sinaimg.cn/large/006tKfTcly1ftnbdr0yg5j30au078aaf.jpg)

* CSS选择器的语法规则

  ![img](https://ws4.sinaimg.cn/large/006tKfTcly1ftnbi5yxaaj30le04c0tf.jpg)

  ![img](https://ws1.sinaimg.cn/large/006tKfTcly1ftnbjot2cdj30ld0n80y2.jpg)

  ![img](https://ws4.sinaimg.cn/large/006tKfTcly1ftnblw5mb1j30lq02wgm4.jpg)

### 2.3 爬虫的基本原理

* 爬虫概述：爬虫就是获取网页并提取和保存信息的自动化程序。
  1. 获取网页：获取网页的源代码，并从源代码中提取想要的信息
  2. 提取信息：分析网页源代码，从中提取我们想要的数据。
     * 正则表达式提取，这是一个万能的方法，但是在构造时比较复杂且易出错。
     * 根据网页节点属性、CSS选择器或XPath来提取网页信息的库：如Beautiful Soup、pyquery、lxml。
  3. 保存数据：可以简单保存为文本或JSON文本，也可以保存到数据库，如MySQL和MongoDB等，也可以保存至远程服务器。
  4. 自动化程序：爬虫可以替代我们来完成爬取工作的自动化程序，他可以在爬取过程中进行各种异常处理、错误重试等操作，以确保爬取持续高效地运行。

* 能抓怎样的数据：HTML源代码、二进制数据、JSON字符串等，只要在浏览器里面可以访问得到，就可以将其抓取下来。

* JavaScript渲染页面

  网页越来越多地采用Ajax、前端模块化工具来构建，整个网页可能都是由JavaScript渲染出来的，原始的HTML代码就是一个空壳。使用urlib或requests请求当前页面时，我们只能得到这个HTML代码，它不会帮助我们去继续加载这个JavaScript文件。

  * 解决方法
    * 分析Ajax接口
    * 使用Selenium、Splash等库实现模拟JavaScript渲染

### 2.4 会话和Cookies

#### 无状态HTTP

HTTP协议对事务处理是没有记忆能力的，即服务器不知道客户端是什么状态。当我们向服务器发送请求后，服务器解析请求，然后返回对应的响应，服务器负责完成这个过程，该过程是完全独立的，服务器不会记录前后状态的变化，缺少状态记录。若后续需要处理前面的信息，则必须重传，这导致需要额外传递一些前面的重复请求，才能获取后续响应。

会话和Cookies可以保持HTTP连接的状态，会话在服务端，Cookies在客户端。浏览器在下次访问网页时会自动附带上Cookies发送给服务器，服务器通过识别Cookies并鉴定出是哪个用户，然后再判断用户是否是登录状态，然后返回对应的响应。

* 会话：在Web中，会话对象用来存储特定用户会话所需的属性及配置信息。当用户在应用程序的Web也之间跳转存储在会话对象中的变量将不会丢失，而是在用户会话中一直存在下去。当用户请求来自应用程序的Web页时，如果该用户还没有会话，则Web服务器自动创建一个会话对象。当会话过期或被放弃后，服务器将终止该会话。
* Cookies：Cookies指某些网站为了辨别用户身份、进行会话跟踪而存储在用户本地端上的数据。
  * 会话维持
  * 属性结构
    * Name：Cookies的名称，一旦创建不可更改
    * Value：该Cookies的值。如果值为Unicode字符，需要为字符编码。如果为二进制数据，则需要用BASE64编码
    * Domain：可以访问该Cookie的域名
    * Max Age：Cookie失效的时间，单位为秒，若为正数，则Cookie在Max Age秒之后失效。若为负数，关闭浏览器即失效。
    * Path：该Cookie的使用路径。若设置为/，则本域名下所有页面都可以访问该Cookie
    * Size：Cookie的大小
    * HTTP：Cookie的httponly属性。若为True，则只有在HTTP头中带有此Cookie的信息，而不能通过document.cookie来访问此Cookie
    * Secure：该Cookie是否仅被使用安全协议传输。安全协议有HTTPS和SSL等，在网络上传输数据之间先将数据加密。默认为false
* 常见误区
  * 除非程序通知服务器删除一个会话，否则服务器会一直保留。
  * 关闭浏览器不会导致会话被删除，这就需要服务器为会话设置一个失效时间，当距离客户端上一次使用会话的时间超过这个失效时间时，服务器就可以认为客户端已停止活动，然后才会将会话删除。

### 2.5 代理的基本原理

#### 基本原理

代理实际上是指代理服务器，英文叫作proxy server，他的功能是代理网络用户去取得网络信息。形象地说，它是网络信息的中转站。如果设置了代理服务器，本机不是直接向Web服务器发起请求，而是向代理服务器发出请求，请求会发送给代理服务器，然后代理服务器再发送给Web服务器，接着由代理服务器再把Web服务器返回的响应转发给本机。

* 作用

  * 突破IP访问限制，访问一些平时不能访问的站点
  * 访问一些单位或团体内部资源：比如使用教育网内地址段免费代理服务器，就可以对教育网开放的各类FTP下载上传，以及各类资料查询共享等服务
  * 提高访问速度：通常代理服务器都设置一个较大的硬盘缓冲区，当有外接的信息通过时，同时也将其保存在缓冲区中，当其他用户再访问相同的信息时，则直接由缓冲区中取出信息，传给用户，以提高访问速度。
  * 隐藏真实IP

* 爬虫代理

  对于爬虫来说，由于爬虫爬取速度过快，在爬取过程中可能遇到同一个IP访问过于频繁的问题，此时网站就会让我们输入验证码登录后者直接封锁IP。

  使用代理隐藏真实的IP，让服务器以为是代理服务器在请求自己。这样再爬取过程中通过不断更换代理，就不会被封锁。

* 代理分类

  * 根据协议
    * FTP代理服务器：主要用于访问FTP服务器，一般有上传、下载及缓存功能，端口一般为21、2121等
    * HTTP代理服务器：主要用于访问网页，一般有内容过滤和缓存功能，端口一般为80、8080、3128
    * SSL/TLS代理：主要用于访问加密网站，一般有SSL或TLS加密功能（最高支持128位加密强度），端口一般为443
    * RTSP代理：主要用于访问Real流媒体服务器，一般有缓存功能，端口一般为554
    * Telnet代理：主要用于telnet远程控制（黑客入侵计算机时常用语隐藏身份），端口一般为23
    * POP3/SMTP代理：主要用户POP3/SMTP方式收发邮件，一般有缓存功能，端口一般为110/25
    * SOCKS代理：单纯传递数据包，速度快，一般有缓存功能，端口一般为1080
      * SOCKS4：只支持TCP
      * SOCKS5：支持TCP和UDP，还支持各种身份验证机制、服务器域名解析等
  * 根据匿名程度
    * 高度匿名代理：数据包原封不动地转发
    * 普通匿名代理：会在数据包上做一些改动，服务端有可能发现这个是代理服务器，也有一定几率追查到真实IP。代理服务器通常会加入的HTTP头有HTTP_VIA和HTTP_X_FORWARDED_FOR
    * 透明代理：不但改动数据包，还有告诉服务器客户端的真实IP。这种代理除了能用缓存技术提高浏览速度，能将内容过滤提高安全性之外，并无其他显著作用，最常见的例子是内网中的硬件防火墙
    * 间谍代理：指组织或个人创建的用于记录用户传输的数据，然后进行研究、监控等目的的代理服务器

* 常见代理设置

  * 使用网上的免费代理
  * 使用付费代理服务
  * ADSL拨号

## 三、基本库的使用

### 3.4 抓取猫眼电影排行

* 目标：提取出猫眼电影TOP100的电影名称、时间、评分、图片等信息，提取的站点URL为http://maoyan.com/board/4，提取结果 会以文件形式保存下来。

* 分析

  * 目标站点：http://maoyan.com/board/4
  * 第二页：http://maoyan.com/board/4?offset=10

  1. 抓取首页实现get_one_page(url)

  2. 正则表达式提取：

     ```python
     '\<dd>.*?board-index.*?>(.*?)\</i>.*?data-src="(.*?)".*?name.*?a.*?>(.*?)\</a>.*?"star".*?>(.*?)\</p>.*?"releasetime".*?>(.*?)\</p>.*?"integer".*?>(.*?)\</i>.*?"fraction".*?>(.*?)\</i>.*?\</dd>'
     ```

  3. 写入文件

  4. 分页爬取

  5. 运行代码

* 代码

```python
import requests
import re
from requests.exceptions import RequestException
import json
from multiprocessing import Pool

def get_one_page(url):
    try:
        headers = {
            'User-Agent':'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.99 Safari/537.36'
        }
        response = requests.get(url,headers=headers)
        if response.status_code == 200:
            return response.text
        return None
    except RequestException:
        return None

def parse_one_page(html):
    pattern = re.compile('<dd>.*?board-index.*?>(.*?)</i>.*?data-src="(.*?)".*?name.*?a.*?>(.*?)</a>.*?"star".*?>(.*?)</p>.*?"releasetime".*?>(.*?)</p>.*?"integer".*?>(.*?)</i>.*?"fraction".*?>(.*?)</i>.*?</dd>',re.S)
    items = re.findall(pattern,html)
    for item in items:
        yield {
            'index':item[0],
            'image':item[1],
            'title':item[2],
            'actor':item[3].strip()[3:],
            'time':item[4].strip()[5:],
            'score':item[5] + item[6]
        }

def write_to_file(content):
    with open('result.txt','a',encoding='utf-8') as f:
        f.write(json.dumps(content,ensure_ascii=False) + '\n')
        f.close()


def main(offset):
    url = 'http://maoyan.com/board/4?offset=' + str(offset)
    html = get_one_page(url)
    for item in parse_one_page(html):
        write_to_file(item)
        print(item)
    # print(html)


if __name__ == '__main__':

    pool = Pool()
    pool.map(main,[i * 10 for i in range(10)])

```

### 练习：抓取豆瓣top250电影排行

```python
import requests
from requests.exceptions import RequestException
import re
import json
from multiprocessing import Pool

def get_one_page(url):
    try:
        headers = {
            'User-Agent':'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.99 Safari/537.36'
        }
        response = requests.get(url,headers=headers)
        if response.status_code == 200:
            return response.text
        return None
    except RequestException:
        return None

def parse_one_page(html):
    pattern = re.compile('<li>.*?class="">(.*?)</em>.*?"title">(.*?)</span>.*?average">(.*?)</span>.*?inq">(.*?)</span>.*?</li>',re.S)
    items = re.findall(pattern,html)
    for item in items:
        yield {
            'index':item[0],
            'title':item[1],
            'score':item[2],
            'quote':item[3]
        }

def write_to_file(content):
    with open('douban.txt','a',encoding='utf-8') as f:
        f.write(json.dumps(content,ensure_ascii=False) + '\n')
        f.close()

def main(start):
    url = "https://movie.douban.com/top250?start=" + str(start)
    html = get_one_page(url)
    for item in parse_one_page(html):
        # print(item)
        write_to_file(item)

if __name__ == '__main__':
    # for i in range(10):
    #     main(i * 25)
    pool = Pool()
    pool.map(main, [i * 25 for i in range(10)])

```





## 四、解析库的使用

## 五、数据存储

### 5.1 文件存储

#### TXT存储

* 实例：保存知乎上“发现”页面的“热门话题”部分，将其问题和答案统一保存成文本形式

* 使用requests获取网页源代码，使用pyquery解析库解析

  ```python
  import requests
  from pyquery import PyQuery as pq
  
  url = 'https://www.zhihu.com/explore'
  headers = {
  	'User-Agent':'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.99 Safari/537.36'
  }
  html = requests.get(url,headers=headers).text
  file_html = open('explore.html','a',encoding='utf-8')
  file_html.write(html)
  file_html.close()
  doc = pq(html)
  items = doc('.explore-tab .feed-item').items()
  for item in items:
  	question = item.find('h2').text()
  	author = item.find('.author-link-line').text()
  	answer = pq(item.find('.content').html()).text()
  	file = open('explore.txt','a',encoding='utf-8')
  	file.write('\n'.join([question,author,answer]))
  	file.write('\n' + '=' * 50 + '\n')
  	file.close()
  ```

* 打开方式

  * r：以只读方式打开文件，文件指针将会放在文件的开头，默认模式
  * rb：以二进制只读方式打开，指针放在开头
  * r+：以读写方式打开。指针放在开头
  * rb+：以二进制读写方式打开，指针放在开头
  * w：以写入方式打开，若文件已存在，则覆盖，若文件不存在，则创建新的文件
  * wb：以二进制写入方式打开，则覆盖，若文件不存在，则创建新的文件
  * w+：以读写方式打开，若文件已存在，则覆盖，若文件不存在，则创建新的文件
  * wb+：以二进制读写方式打开，若文件已存在，则覆盖，若文件不存在，则创建新的文件
  * a：以追加方式打开，若该文件已存在，文件指针将会放在文件结尾。即新的内容会被写入到已有内容之后，若文件不存在，则创建新的文件写入
  * ab：以二进制追加方式打开，若该文件已存在，文件指针将会放在文件结尾。即新的内容会被写入到已有内容之后，若文件不存在，则创建新的文件写入
  * a+：以读写方式打开一个文件，若该文件已存在，文件指针将会放在文件结尾。文件打开时会是追加模式，若文件不存在，则创建新的文件写入
  * ab+：以二进制追加方式代开，若该文件已存在，文件指针将会放在文件结尾。即新的内容会被写入到已有内容之后，若文件不存在，则创建新的文件写入

* 简化写法

  * with as语法，在with控制块结束时，文件会自动关闭，就不需要再调用close()方法了

    ```python
    with open('explore.txt','a',encoding='utf-8') as file:
        file.write('\n'.join([question,author,answer]))
        file.write('\n' + '=' *50 + '\n')
    ```

#### JSON文件存储

> JSON，全称JavaScript Object Notion，也就是JavaScript对象标记，它通过对象和数组的组合来表示数据，是一种轻量级的数据交换格式。

* 对象和数组

  * 对象：使用{}包裹起来的内容，数据结构为{key1:value1,key2:value2,…}的键值对结构。在面向对象的语言中，key为对象的属性，value为对应的值。键名可以使用整数和字符串表示。值得类型可以使任意类型。
  * 数组：使用[]包裹起来的内容，数据结构为["java","javascritpt","vb",…]的索引结构。在JavaScript中，数组是一种比较特殊的数据类型，它也可以像对象那样使用键值对，但还是索引用的多。同样，值可以是任意类型。

  ```json
  [
      {
          "name":"bob",
          "gender":"male",
          "birthday":"today"
      },
      {
          "name":"selina",
          "gender":"female",
          "birthday":"tomorrow"
      }
  ]
  ```

* 读取JSON：通过dumps()方法将JSON对象转为文本字符串

  ```python
  import json
  
  str = '''
  [
      {
          "name":"bob",
          "gender":"male",
          "birthday":"today"
      },
      {
          "name":"selina",
          "gender":"female",
          "birthday":"tomorrow"
      }
  ]
  '''
  print(type(str))
  data = json.loads(str)
  print(data)
  print(type(json))
  
  #添加索引获得字典元素，通过调用键名即可得到键值
  data[0]['name']
  data[0].get('name')
  data[0].get('age') # None
  data[0].get('age',25) # default value = 25
  
  # 从JSON文本读取内容
  with open('data.json','r') as file:
      str = file.read()
      data = json.loads(str)
      print(data)
      
  ```

  > JSON的数据需要用双引号来保卫，不能使用单引号，否则会出现JSONDecodeError错误

* 输出JSON：调用dumps()方法将JSON对象转换为字符串

  ```python
  import json
  
  data = [{
      'name':'王伟',
      'gender':'male',
      'birthday':'19920825'
  }]
  # 为了输出中文，还需要指定参数ensure_ascii=False,参数indent，代表缩进字符个数，另外还要规定文件输出的编码
  with open('data.json','w',encoding='utf-8') as file:
      file.write(json.dumps(data,indent=2,ensure_ascii=False))
  ```

#### CSV文件存储

> CSV，全称Comma-Separated Values，中文可以叫作逗号分隔值或字符分隔值，其文件以纯文本形式存储表格数据。该文件是一个字符序列，可以由任意数目的记录组成，记录间以某种换行符分隔。

* 写入

```python
import csv

# delimiter可以修改列与列之间的分隔符，writerrows可以同时写入多行，此时参数就需要为二位列表
with open('data.csv','w') as csvfile:
    writer = csv.writer(csvfile,delimiter=' ')
    writer.writerrow('id','name','age')
    writer.writerrows([['1001','mike',20],['1002','bob',22]])
    
# 写入字典
import csv

with open('data.csv','w',encoding='utf-8') as csvfile:
    fieldnames = ['id','name','age']
    writer = csv.DictWriter(csvfile,fieldnames=fieldnames)
    writer.writeheader()
    writer.writerow({'id':'1001','name':'mike','age':20})
    writer.writerows([{'id':'1002','name':'bob','age':21},{'id':'1003','name':'du','age':25}])
    
```

* 读取

  > 这里构造的Reader对象，通过遍历输出了每行的内容，每一个行都是一个列表形式。如果文件中包含中文的话，还需要指定文件编码。

  ```python
  with open('data.csv','r',encoding='utf-8') as csvfile:
      reader = csv.reader(csvfile)
      for row in reader:
          print(row)
  ```

  * 也可以使用pandas中的read_csv()方法将数据从CSV中读取出来

    ```python
    import pandas as pd
    
    df = pd.read_csv('data.csv')
    print(df)
    ```

### 5.2 关系型数据库存储

> 关系型数据库是基于关系模型的数据库，关系模型是通过二维表来保存的，所以它的存储方式就是行列组成的表，每一列就是一个字段，每一行就是一条记录。表可以看作某个实体的集合，而实体之间也存在联系，这就需要表与表之间的联系关系来体现，如主键外键的关联关系。多个表组成一个数据库，也就是关系型数据库。
>
> 关系型数据库有多种，如SQLite、MySQL、Oracle、SQL Server、DB2等。

#### MySQL存储

* 连接数据库

  ```python
  import pymysql
  
  # 通过PyMySQL的connect()方法声明一个MySQL连接duixiangdb
  db = pymysql.connect(host='localhost',user='root',password='',port=3306)
  # 连接成功后调用cursor()获取MySQL的操作游标
  cursor = db.cursor()
  # execute()方法执行sql语句
  cursor.execute('SELECT VERSION()')
  # 返回执行结果
  data = cursor.fetchone()
  print('Database version:',data)
  cursor.execute('CREATE DATABASE spiders DEFAULT CHARACTER SET UTF8')
  db.close()
  ```

* 创建表

  ```python
  import pymysql
  
  # 代码格式化 command + alt + L
  db = pymysql.connect(host='localhost', user='root', password='', port=3306, db='spiders')
  cursor = db.cursor()
  sql = 'CREATE TABLE IF NOT EXISTS students (id VARCHAR(255) NOT NULL ,name VARCHAR(255) NOT NULL,age INT NOT NULL,PRIMARY KEY (id))'
  cursor.execute(sql)
  db.close()
  ```

* 插入数据

  ```python
  import pymysql
  
  id = '20120001'
  user = 'bob'
  age = 20
  
  db = pymysql.connect(host='localhost', user='root', password='', port=3306, db='spiders')
  cursor = db.cursor()
  # 使用构造SQL语句：sql = 'INSERT INTO student(id,name,age) values(' + id + ', ' + name + ', ' + age + ')'
  # 使用格式化符%s实现，可以避免字符串拼接的麻烦，又可以避免引号冲突的问题
  sql = 'INSERT INTO students(id,name,age) values(%s,%s,%s)'
  try:
      cursor.execute(sql,(id,user,age))
      # 需要执行db对象的commit()方法才可实现数据插入，该方法可以将语句提交到数据库执行的方法
      # 对于数据插入、更新、删除操作，都需要调用该方法才能生效
      db.commit()
  except:
      # 如果执行失败，则调用rollback()执行数据回滚
      db.rollback()
  finally:
      db.close()
  ```

* 事务的4个属性（ACID）

  |         属性          | 解释                                                         |
  | :-------------------: | :----------------------------------------------------------- |
  |  原子性（atomicity）  | 事务是一个不可分割的工作单位，事务中包括的诸操作要么都做，要么都不做 |
  | 一致性（consistency） | 事务必须使数据库从一个一致性状态变到另一个一致性状态。一致性与原子性是密切相关的 |
  |  隔离性（isolation）  | 一个事务的执行不能被其他事务干扰，即一个事务内部的操作及使用的数据对并发的其他事务是隔离的，并发执行的各个事务之间不能相互干扰 |
  | 持久性（durability）  | 持久性也称永久性（permanence），指一个事务一旦提交，它对数据库的改变就应该是永久的。接下来的其他操作或故障不应该对其有任何影响 |

  ```python
  import pymysql
  
  db = pymysql.connect(host='localhost', user='root', password='', port=3306, db='spiders')
  cursor = db.cursor()
  # 优化
  data = {
      'id':'20120002',
      'name':'bob',
      'age':20
  }
  table = 'students'
  keys = ', '.join(data.keys())
  values = ', '.join(['%s'] * len(data))
  sql = 'INSERT INTO {table}({keys}) VALUES ({values})'.format(table=table,keys=keys,values=values)
  try:
      if cursor.execute(sql,tuple(data.values())):
          print('successful')
          db.commit()
  except:
      print('failed')
      db.rollback()
  finally:
      db.close()
  ```

* 更新数据

  ```python
  import pymysql
  
  db = pymysql.connect(host='localhost', user='root', password='', port=3306, db='spiders')
  cursor = db.cursor()
  
  data = {
      'id':'20120001',
      'name':'bob',
      'age':25
  }
  
  table = 'students'
  keys = ', '.join(data.keys())
  values = ', '.join(['%s'] * len(data))
  
  # ON DUPLICATE KEY UPDATE 如果主键存在，就执行更新操作
  sql = 'INSERT INTO {table}({keys}) VALUES({values}) ON DUPLICATE KEY UPDATE'.format(table=table,keys=keys,values=values)
  update = ','.join([" {key} = %s".format(key = key) for key in data])
  sql += update
  # 若执行更新操作，则sql语句就是
  # INSERT INTO students(id, name, age) VALUES(%s, %s, %s) ON DUPLICATE KEY UPDATE id = %s, name = %s, age = %s
  # 这里就变成了6个%s，所以在后面的excute()方法的第二个参数元组就需要乘以2编程原来的2倍
  try:
      print(sql)
      if cursor.execute(sql,tuple(data.values()) * 2):
          print('successful')
          db.commit()
  except:
      print('failed')
      db.rollback()
  finally:
      db.close()
  ```

* 删除数据

  ```python
  table = 'students'
  condition = 'age > 20'
  
  # 因为删除条件有多种多样，所以不再继续构造复杂的判断性。这里之间将条件当做字符串来传递，以实现删除操作
  sql = 'DELETE FROM {table} WHERE {condition}'.format(table=table,condition=condition)
  try:
      cursor.excute(sql)
      db.commit()
  except:
      db.rollback()
  finally:
      db.close
  ```

* 查询数据

  ```python
  import pymysql
  
  db = pymysql.connect(host='localhost', user='root', password='', port=3306, db='spiders')
  cursor = db.cursor()
  
  sql = 'SELECT * FROM students WHERE age >= 19'
  try:
      cursor.execute(sql)
      print('Count:',cursor.rowcount)
      # 内部有一个偏移指针用来指向查询结果，最开始偏移指针指向第一条数据，取一次以后，指针指向下一条数	   据，这样再取得话，就会取到下一条数据
      # one = cursor.fetchone()
      # print('One:',one)
      result = cursor.fetchall()
      print('Result:',result)
      print('Result Type:',type(result))
      for row in result:
          print(row)
  except:
      print("Error")
  finally:
      db.close()
      
  # 结果：
  Count: 2
  One: ('20120001', 'bob', 25)
  Result: (('20120002', 'bob', 20),)
  Result Type: <class 'tuple'>
  ('20120002', 'bob', 20)
  ```


### 非关系型存储

> NoSQL，全称Not Only SQL，意为不仅仅是SQL，泛指非关系型数据库。NoSQL是基于键值对的，而且不需要经过SQL层的解析，数据之间没有耦合性，性能非常高。

* 分类
  * 键值存储数据库：Redis、Voldemort和Oracle BDB等
  * 列存储数据库：Cassandra、HBase和Riak等
  * 文档型数据库：CouchDB和MongoDB等
  * 图形数据库：Neo4J、InfoGrid和Infinite Graph等

#### MongoDB存储

* 连接MongoDB，连接数据库并插入、查询数据

  ```python
  import pymongo
  from pymongo import MongoClient
  
  # 连接数据库
  client = MongoClient('mongodb://localhost:27017/')
  # client = pymongo.MongoClient(host='localhost',prot=27017)
  
  # 指定数据库，两种方式等价
  # db = client.test
  db = client['test']
  
  # 指定集合
  # collection = db.student
  collection = db['student']
  
  # 插入数据
  student = {
      'id':'20170101',
      'name':'jordan',
      'age':20,
      'gender':'male'
  }
  
  student1 = {
      'id':'20170102',
      'name':'mike',
      'age':20,
      'gender':'male'
  }
  
  student2 = {
      'id':'20170103',
      'name':'du',
      'age':20,
      'gender':'male'
  }
  
  # 插入一条数据并返回_id值
  # result = collection.insert_one(student)
  # print(result.inserted_id)
  
  # 插入多条数据
  # result = collection.insert_many([student1,student2])
  # print(result.inserted_ids)
  
  # 查询数据 利用find_one()或find()方法进行查询
  result = collection.find_one({'name':'mike'})
  print(type(result))
  print(result)
  
  results = collection.find({'age':20})
  print(results)
  for r in results:
      print(r)
  
  # 查询年龄大于20的数据
  results = collection.find({'age':{'$gt':19}})
  print(results)
  for r in results:
      print(r)
  ```

* 查询符号表

  ![img](https://ws4.sinaimg.cn/large/006tNc79ly1fteyfoplygj30ml06ngmq.jpg)

  ![img](https://ws2.sinaimg.cn/large/006tNc79ly1fteyjn2frlj30ml06eq4b.jpg)

* 计数

  ```python
  count = collection.find().count()
  print(count)
  
  count = collection.find({'age':20}).count()
  print(count)
  ```

* 排序

  ```python
  # 升序：pymongo.ASCENDING 降序：pymongo.DESCENDING
  results = collection.find.sort('name',pymongo.ASCENDING)
  print([result['name'] for result in results])
  ```

* 偏移

  ```python
  # 忽略前两个元素
  results = collection.find().sort('name',pymongo.ASCENDING).skip(2)
  print([result['name'] for result in results])
  
  # 忽略前两个元素并只取2个元素结果
  results = collection.find().sort('name',pymongo.ASCENDING).skip(2).limit(2)
  print([result['name'] for result in results])
  ```

* 更新

  ```python
  # 更新数据
  condition = {'name':'du'}
  student = collection.find_one(condition)
  student['age'] = 25
  # 建议使用update_one或update_many
  # result = collection.update(condition,student)
  # 也可以使用$set操作符对数据进行更新，这样可以只更新student字典内存在的字段，如果原先还有其他字段，则不会更新也不会删除。
  # result = collection.update(condition,{'$set':student})
  print(result)
  
  condition = {'name':'mike'}
  student = collection.find_one(condition)
  student['age'] = 26
  result = collection.update_one(condition,{'$set':student})
  print(result)
  print(result.matched_count,result.modified_count)
  
  condition = {'age':{'$gt':20}}
  # 第一条符合条件的年龄+1
  # result = collection.update_one(condition,{'$inc':{'age':1}})
  result = collection.update_many(condition,{'$inc':{'age':1}})
  print(result)
  print(result.matched_count,result.modified_count)
  ```

* 删除

  ```python
  # 删除
  result = collection.delete_one({'name':'mike'})
  print(result)
  print(result.deleted_count)
  result = collection.delete_many({'age':20})
  print(result)
  print(result.deleted_count)
  ```

* 其他方法

  * find_one_and_delete()、finde_one_and_replace()和find_one_and_update()等
  * create_index()、create_indexes()和drop_index()等
  * 操作指南：https://docs.mongodb.com/guides/
  * PyMongo官方文档：http://api.mongodb.com/python/current/api/pymongo/collection.html

#### Redis存储

> Redis是一个基于内存的高效的键值型非关系型数据库，存取效率极高，而且支持多种存储数据结构，使用简单。

* 启动redis服务端

  ```bash
  # 启动redis数据库服务端
  redis-server
  # 使用密码启动redis客户端
  redis-cli -a 1234
  ```

* Redis和StrictRedis

  redis-py库提供两个类Redis和StrictRedis来实现Redis的命令操作（官方推荐使用StrictRedis）

* 连接Redis

  ```python
  from redis import StrictRedis,ConnectionPool
  
  # 使用ConnectionPool连接
  pool = ConnectionPool(host='localhost',port=6379,db=0,password='1234')
  
  ''''
  # ConnectionPool还支持通过URL来构建
  # Redis TCP连接
  redis://[:passwrod]@host:port/db
  
  # Redis TCP+SSL连接
  rediss://[:passwrod]@host:port/db
  
  # Reids UNIX socket连接
  unix://[:password]@path/to/socket.sock?db=db
  
  url = 'redis://:1234@localhost:6379/0'
  pool = ConnectionPoo;.from_url(url)
  redis = StrictRedis(connection_pool=pool)
  '''
  # redis = StrictRedis(host='localhost',port=6379,db=0,password='1234')
  
  redis = StrictRedis(connection_pool=pool)
  redis.set('name','duzhida')
  print(redis.get('name'))
  ```

  

## 六、Ajax数据爬取

### 什么是Ajax

> Ajax全称为Asynchronous JavaScript and XML，即异步的JavaScript和XML。它不是一门编程语言，而是利用JavaScript在保证页面不被刷新，页面链接不改变的情况下与服务器交换数据并更新部分网页的的技术。

#### 基本原理

* 发送Ajax请求到网页更新的过程分为以下3步：

  1. 发送请求
  2. 解析内容
  3. 渲染网页

* 发送请求

  ```javascript
  // 这个JavaScript对Ajax最底层的实现，实际上就是新建了XMLHttpReequest对象，然后调用onreadystatechange属性设置了监听，然后调用open()和send()方法向某个链接(服务器)发送请求
  var xmlhttp;
  if(window.XMLHttpRequest){
      //code for IE7+,Firfox,Chrome,Opera,Safari
      xmlhttp = new XMLHttpRequest();
  }else{
      //code for IE6,IE5
      xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
  }
  
  xmlhttp.onreadystatechange=function(){
      if(xmlhttp.readyState == 4 && xmlhttp.status == 200){
          document.getElementById("myDiv").innerHTML = xmlhttp.responseText;
      }
  }
  xmlhttp.open("POST","/ajax/",true);
  xmlhttp.send()
  ```

* 解析内容

  得到相应之后，onreadystatechange属性对应的方法就会触发，此时利用xmlhttp的responseText属性便可取到响应内容。返回的内容可能是HTML，可能是JSON，接下来只需要在方法中用JavaScript进一步处理即可。

* 渲染网页

  JavaScript有改变网页内容的能力，解析完响应内容之后，就可以调用JavaScript来针对解析完的内容对网页进行下一步处理。比如，通过document。getElementById().innerHTML就可以对元素内的源代码进行更改。这样网页显示的内容就改变了，这样的操作也被称为DOM操作。

### Ajax分析方法

1. 查看请求
2. 过滤请求

## 七、动态渲染页面爬取

## 八、验证码识别

### 8.1 图形验证码的识别



## 九、代理的使用

## 十、模拟登陆

## 十一、APP的爬取

## 十二、 pyspider框架的使用

* 相关链接
  * GItHub地址：https://github.com/binux/pyspider
  * 官方文档：http://docs.pyspider.org/en/latest/
* 基本功能
  * 提供方便易用的WebUI系统，可视化编写和调试爬虫
  * 提供爬取进度监控、爬取结果查看、爬虫项目管理等功能
  * 支持多种后端数据库，如MySQL、MongoDB、Redis、SQLite、Elasticsearch、PostgreSQL
  * 支持多种消息队列，如RabbitMQ、Beanstalk、Redis、Kombu
  * 提供优先级控制、失败重试、定时抓取等功能
  * 对接了PhantomJS，可以爬取JavaScript渲染的页面
  * 支持单机和分布式部署，支持Docker部署
* 与Scrapy比较
* 架构
* 基本使用
  * 目标：爬去去哪儿网的旅游攻略，链接为http://travel.qunar.com/travelbook/list.htm

## 十三、Scrapy框架的使用

## 十四、分布式爬虫

## 十五、分布式爬虫的部署



