# Scrapy框架随机伪装设置


### 随机请求头设置：
##### 方法一：
定义一个存放请求头的列表，并从中随机获取请求头：

获取请求头的网址http://www.useragentstring.com/pages/useragentstring.php?name=All 
```
import random
class UserAgentDownloadMiddleware(object):
    USER_AGENTS = [
        'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36',
        'Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.36 (KHTML like Gecko) Chrome/44.0.2403.155 Safari/537.36',
        'Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2228.0 Safari/537.36',
        'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2227.1 Safari/537.36',
        'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2227.0 Safari/537.36',
        'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2227.0 Safari/537.36',
        'Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2226.0 Safari/537.36',
        'Mozilla/5.0 (Windows NT 6.4; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2225.0 Safari/537.36',
        'Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2225.0 Safari/537.36',
        'Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2224.3 Safari/537.36',
        'Mozilla/5.0 (Windows NT 10.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/40.0.2214.93 Safari/537.36',
        'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/37.0.2062.124 Safari/537.36'
    ]
 
    def process_request(self,request,spider):
        user_agent = random.choice(self.USER_AGENTS)
        request.headers['User-Agent'] = user_agent
```


##### 方法二
通过fake_useragent模块随机获取请求头
```
from fake_useragent import UserAgent
class UserAgentDownloadMiddleware(object):
    def process_request(self,request,spider):
        user_agent = UserAgent().random
        request.headers['User-Agent'] = user_agent
```
<br><br><br>

### 随机IP代理：
##### 一、把随机的IP列表定义在settings.py文件里面
```
PROXIES=['http://180.119.43.106:4228', 'http://106.56.246.104:4237', 'http://118.79.56.240:4278',
         'http://223.215.175.132:4272', 'http://115.221.10.97:2316', 'http://182.87.239.182:4250',
         'http://113.138.170.34:4659', 'http://182.246.158.172:4263', 'http://183.166.138.236:4248',
         'http://114.237.230.132:2444', 'http://175.175.150.202:4211', 'http://124.112.214.13:4286',
         'http://114.239.172.198:4236', 'http://110.19.188.168:6410', 'http://182.99.234.158:1659',
         'http://182.108.168.170:4234', 'http://49.84.32.34:4203', 'http://121.226.45.229:8736',
         'http://115.220.38.159:4208', 'http://118.79.9.64:6996']
```


##### 二、在middleware文件里面添加一个代理中间件
```
import random
class PorxyMiddleware(object):
    #设置Proxy
    def __init__(self,ip):
        self.ip=ip
    @classmethod
    def from_crawler(cls,crawler):
        return cls(ip=crawler.settings.get('PROXIES'))
 
    def process_request(self,request,spider):
        ip =random.choice(self.ip)
        request.meta['proxy'] = ip
```


##### 三、在settings文件里面的下载器中间键启动自己定义的类
```
DOWNLOADER_MIDDLEWARES = {
    'dome1.middlewares.ProxyMiddleware':543
}
```
<br><br><br>
