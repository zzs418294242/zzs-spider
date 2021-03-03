# wechatPubSpider
> 微信公众号爬虫：微信搜狗引擎每个公众号爬取10条最近的文章；所以为了爬取喜欢的所有的公众文章，抓取微信公众号，主要需要两个主要参数:1. __biz(微信公众号id),2.wap_sid2(类似于获取公众号单一文章的权限)。

- 1.获取公众号id:
	- 随意输入关键词，然后获取关键词相关的微信公众号，接着获取微信公众号id。微信公众号id的获取首先是从搜索引擎微信公众号搜索获取。获得公众号：首先用搜狗输入关键词获得你要的微信公众号。通过检索关键字，在搜索目录获取公众号序列表。点击微信公众号获取单个公众号的链接。
	- 进入单个微信公众号，然后获取其中的页面的代码。在其中的javascript中存在这个公众号的__biz（微信公众号id）
  ```
     <script type="text/javascript">
     document.domain="qq.com";
     var biz = "**MzI3MTA2OTkxNQ**==" || "";
     var src = "3" ; 
     var ver = "1" ; 
     var timestamp = "1507726402" ; 
     var signature = "**MgPVC3IPsaxxEYqtBq2IOampNVHLxE*D2-f9b*rLZKzoGtUHRNbDczmbZCSVr2xU0so04b-YJ5*pnPENrnDsMg=="** ; 
     var name="java--demon"||"xxxx";
    
  
  ``` 
- 2.wap_sid2单一公众号的所有文章获取的权限值。
	- wap_sid2参数值的获取需要通过微信手机客户端app，从中获取其权限。

- 3.使用方法：
	- wechatPubSpider/wechatSpider -/wechatSpider/目录下面的settings文件，MONGO_DATABASE，MONGO_URI，MONGO_USER，MONGO_PASS分别填写数据库，项目保存数据的地址IP，用户以及密码。
	- wechatPubSpider/wechatSpider -/wechatSpider/spiders/目录下面settings文件,MONGO_URI，MONGO_DATABASE,MONGO_USER,MONGO_PASS,ARTICLE,WECHATID,RESPONSE，其中不同的，是数据库里面的collectionName，可以随意起喜欢的名字。
- 4.启用顺序：
	- 运行wechat.py文件，然后输入关键词，获取微信公众号ID。存入MongoDB数据库。
	```
	$ scrapy crawl wechat
	```
	- 运行getSession.py文件，获取权限值wap_sid2，并把biz与wap_sid2对应入库。
	```
	$ scrapy crawl getSession
	```
	- 运行data.py文件，爬取数据，存入数据库。
	```
	$ scrapy crawl data
	```

