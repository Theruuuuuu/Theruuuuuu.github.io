---
title: "RssCrawler"
date: 2023-05-07T15:42:34+08:00
categories: ["Python","爬蟲","Web"]
tags: ["筆記"]
---
# RSS
RSS是一種統一的格式標準，常被使用新聞、資訊網站，可以讓使用者輕鬆取得最新的資訊。
## 基本格式
以Google News 為例

![成果](/images/RssCrawler/0.png)       
* title : 文章標題
* link : 文章連結
* description : 文章詳細資料
* source : 文章來源
## Feedparser
一個Python library 可以用來解析檔案，RSS是其中一個可以解析的類型。

**使用方式**        

先下載
library
```
pip install feedparser
```

```py
#引入library
import feedparser
#目標網址-GoogleNews-搜尋"台灣"
url = 'https://news.google.com/rss/search?q=%E5%8F%B0%E7%81%A3&hl=zh-TW&gl=TW&ceid=TW%3Azh-Hant'
#解析目標網址
res = feedparser.parse(rss_url)
```

```py
print(res)
```
結果
![成果](/images/RssCrawler/2.png)  
**常用標籤**
* entries : 每篇文章的資訊
    * title : 文章標題
    * title_detail : 標題細節    
    * link : 文章網址
    * id : 文章ID
    * published : 發布日期
```py
for post in rss.entries:
    print(post.title)
    print (post.published )
    print (post.link)
```     
結果

![成果](/images/RssCrawler/3.png)  

## 加上pandas
**完整程式碼**
```py
import feedparser
import pandas as pd
rss_url = 'https://news.google.com/rss/search?q=%E5%8F%B0%E7%81%A3&hl=zh-TW&gl=TW&ceid=TW%3Azh-Hant'
rss = feedparser.parse(rss_url)
#print(rss)
result=[]
for post in rss.entries:
    result.append({
        "title":post.title,
        "date": post.published,
        "link":post.link
    })
df = pd.DataFrame(result)
```
結果        
![成果](/images/RssCrawler/4.png) 
## 結語
RSS讓Python爬蟲簡單了不少，使用這個方式會比一般爬html檔還要還要來的直覺，但是不是每個網站都會提供RSS的服務。