---
title: "【從零開始架設部落格 #3】將自己的部落格加入Google分析"
date: 2021-05-21T00:00:00+08:00
categories:
  - 從零開始架設部落格
tags:
  - Github Pages
  - blog
  - Google Analytics
  - Minimal Mistakes
---

這篇會教你如何在自己網站(Minimal Mistakes)上加入Google分析(Google Analytics)，對使用者操作流量得到更進一步的分析。

## 特色

* 免費
* 設定簡單

## 建置流程

[Google Analytics](http://analytics.google.com/)

### Step1. 帳戶設定

我這邊是填好帳戶名稱後，預設勾底下三個。

![Google Analytics Account Setting](/assets/images/post/2021-05-21-How-to-Add-Google-Analytics-to-blog/1.jpg "Google Analytics Account Setting")

### Step2. 資源設定

資源設定這邊你可以自由設定，但有一些限制，例如:不能純中文等等，我是懶直接設定成網址。

![Google Analytics Resource Setting](/assets/images/post/2021-05-21-How-to-Add-Google-Analytics-to-blog/2.jpg "Google Analytics Resource Setting")

### Step3. 提供商家相關資訊

這裡產業類別我是以部落格主軸去選，因為是個人部落格，所以商家規模選小，然後用途自己勾一勾。

![Google Analytics Resource Setting](/assets/images/post/2021-05-21-How-to-Add-Google-Analytics-to-blog/3.jpg "Google Analytics Resource Setting")

### Step4. 網站串流

這裡要串流到你的網站，然後取得你的評估ID。

![串流設定1](/assets/images/post/2021-05-21-How-to-Add-Google-Analytics-to-blog/4.jpg "串流設定1")

![串流設定2](/assets/images/post/2021-05-21-How-to-Add-Google-Analytics-to-blog/5.jpg "串流設定2")

![串流設定3](/assets/images/post/2021-05-21-How-to-Add-Google-Analytics-to-blog/6.jpg "串流設定3")

### Step5. 將剛剛取得的評估ID加入自己_config.yml

將下面這段Code加入至_config.yml，tracking_id記得替換成自己上面拿到的。
```
analytics:
  provider: "google-gtag"
  google:
    tracking_id: "評估ID"
    anonymize_ip: false # default
```
加入後會像這樣

![程式設定](/assets/images/post/2021-05-21-How-to-Add-Google-Analytics-to-blog/7.jpg "程式設定")

### Step6. 完成

將這個的異動Push到Github後，記得進去網站內操作一下留下紀錄。就能直接在Google分析內看到結果囉。

