# Python网络爬虫开发实战

## 一、开发环境配置

### 1.1 Python3

### 1.2 请求库的安装

### 1.3 解析库的安装

### 1.4 数据库的安装

### 1.5 存储库的安装

### 1.6 Web库的安装

### 1.7 App爬取相关的库安装

### 1.8 爬虫框架的安装

### 1.9 部署库相关的库的安装

## 二、爬虫基础

### 2.1 HTTP基本原理

* URI和URL
  * URI全称Uniform Resource Identifier，即统一资源标志符

  * URL全称Universal Resource Locator，即统一资源定位符

  * URL是URI的子集

  *   另一个子类为URN全称Universal Resource Name，即统一资源名称

  *   关系

      ![img](https://ws2.sinaimg.cn/large/006tNc79gy1ft42wp69kxj308704c74c.jpg)

*   超文本(hypertext)，网页就是超文本解析而成的。

*   HTTP和HTTPS

    *   HTTP全称Hyper Text Transfer Protocol，中文名称:超文本传输协议。是用于从网络传输文本数据到本地浏览器的传送协议，它能保证高效而准确地传送超文本文档。
    *   HTTPS全称Hyper Text Transfer Protocol voer Secure  Socket Layer，是以安全为目标的HTTP通道，即HTTP的安全版，HTTP下加入SSL层，简称HTTPS
        *   作用:
            *   建立一个信息安全通道来保证数据传输的安全
            *   确认网站的真实性，凡是使用了HTTPS的网站，都可以通过点击浏览地址栏的锁头标志来查看网站认证之后的真实信息，也可以通过CA机构颁发的安全签章来查询。

*   HTTP请求过程

    *   

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

## 六、Ajax数据爬取

## 七、动态渲染页面爬取

## 八、验证码识别

### 8.1 图形验证码的识别



## 九、代理的使用

## 十、模拟登陆

## 十一、APP的爬取

## 十二、 pyspider框架的使用

## 十三、Scrapy框架的使用

## 十四、分布式爬虫

## 十五、分布式爬虫的部署



