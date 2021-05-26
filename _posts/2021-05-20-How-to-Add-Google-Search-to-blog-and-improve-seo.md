---
title: "【從零開始架設部落格 #2】將自己的部落格加入Google搜尋及優化SEO"
date: 2021-05-20T20:00:00+08:00
categories:
  - 從零開始架設部落格
tags:
  - Github Pages
  - blog
  - Google Search
  - SEO
  - Minimal Mistakes
---

網站架設後，希望自己的網站能在Google搜尋出現，所以使用了Google Search Console，這篇會教你如何使用Google Search Console加入自己網站(Minimal Mistakes)，以提升SEO。

## 特色

* 免費
* 設定簡單

## 建置流程

### Step1. 從Google Search Console加入自己的網站

首先從[Google Search Console](https://search.google.com/search-console/about)加入自己網站，以Github Pages來說，請選右邊這個，如下圖
![Google Search Console](/assets/images/post/2021-05-20-How-to-Add-Google-Search-to-blog-and-improve-seo/1.jpg "Google Search Console")

### Step2. 驗證網站持有人

他會給你一個html檔，請你放在自己的網站底下，放完後再去驗證即可。

### Step3. _config.yml加入Google Search Engine ID

驗證完後他會給一組ID，將這個ID加入_config.yml，如下圖

![Config](/assets/images/post/2021-05-20-How-to-Add-Google-Search-to-blog-and-improve-seo/2.jpg "Config")

```
google:
  search_engine_id: YourID
```

### Step4. 為自己的首頁建立索引

在網站審查這裡輸入自己想要加入索引的網址，記得點測試線上網址，如果都符合會加快處理效率。
![Website Create Index](/assets/images/post/2021-05-20-How-to-Add-Google-Search-to-blog-and-improve-seo/3.jpg "Website Create Index")
### Step5. 完成

如果是網站剛上線或內容不多，會比較晚才出現在網頁搜尋中，記得耐心等待喔。

想要確定可以透過兩種方式

透過url搜尋，但別把協定加進來
```
site:url
```
![Search with site](/assets/images/post/2021-05-20-How-to-Add-Google-Search-to-blog-and-improve-seo/4.jpg "Search with site")

透過網站名稱搜尋
```
網站名稱
```
![Search with name](/assets/images/post/2021-05-20-How-to-Add-Google-Search-to-blog-and-improve-seo/5.jpg "Search with name")

兩種建議都測試過，因為有可能索引將網址加入，但搜尋名稱可能還未加入。

### TroubleShooting

目前網站Sitemap還未提供到Google Search Console，因為Googlebot無法Fetch到，但URL測試工具都可以正常Fetch到，所以目前還在了解中，解決後，會再另外開一篇文章。