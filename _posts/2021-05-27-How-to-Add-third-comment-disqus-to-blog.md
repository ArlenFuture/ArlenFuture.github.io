---
title: "[#4]為自己的部落格加入第三方留言工具Disqus【架設部落格】"
date: 2021-05-27T20:00:00+08:00
categories:
  - 從零開始架設部落格
tags:
  - blog
  - comment
  - Disqus
  - Minimal Mistakes
---

這篇文章會教你如何在 Minimal Mistakes 主題下設定 Disqus 第三方留言工具

## 特色

- 有免費方案
- 設定簡單
- 可多平台登入

## 預先準備

- [Disqus 帳號](https://disqus.com/)

## 建置流程

### Step1. 先建立一個新的 Site

先在首頁點選**GET STARTED**

![Disqus Create a site 1](/assets/images/post/2021-05-27-How-to-Add-third-comment-disqus-to-blog/1.jpg "Disqus Create a site 1")

選**I want to install Disqus on my site**

![Disqus Create a site 2](/assets/images/post/2021-05-27-How-to-Add-third-comment-disqus-to-blog/2.jpg "Disqus Create a site 2")

![Disqus Create a site 3](/assets/images/post/2021-05-27-How-to-Add-third-comment-disqus-to-blog/3.jpg "Disqus Create a site 3")

設定**Website Name**這邊要注意紅圈處，之後會是你的 shortname，以後會拿這個加在\_config.yml。

Category 部分就看自己網站什麼類型的。

Language 的部分，這邊的 Chinese 是簡體中文，我個人不想繁簡混在一起，所以我選英文，你也可以透過其他方式把它繁體化。

### Step2. 額外設定

#### 1. Select Plan.

這邊我是選擇 Basic 的比較沒有要用太進階的功能，也不希望有費用的產生。

![Select Plan.](/assets/images/post/2021-05-27-How-to-Add-third-comment-disqus-to-blog/4.jpg "Select Plan.")

#### 2. Select your platform.

這邊就果斷的選擇 Jekyll，因為本文使用的就是基於 Jekyll 的 Minimal Mistakes。

![Select your platform.](/assets/images/post/2021-05-27-How-to-Add-third-comment-disqus-to-blog/5.jpg "Select your platform.")

#### 3. Jekyll install instructions

之後他就會提供建議的安裝方式，但因為我們使用的是 Minimal Mistakes，安裝方式有些微不同，這邊就由我來提供。

在你的**\_config.yml**加入這幾行。

```yml
# disqus comments
comments:
  provider: "disqus"
  disqus:
    shortname: "your shortname"
```

還有在你的 defaults 的 posts 裡面加入

```yml
comments: true
```

像是這樣

```yml
defaults:
  - scope:
      path: ""
      type: posts
    values:
      comments: true
```

#### 4. Configure Disqus

這邊就提供你一些設定，如果視覺想要固定也可以從底下調整，我是設定 Auto，畫面都挺正常的。

![Configure Disqus](/assets/images/post/2021-05-27-How-to-Add-third-comment-disqus-to-blog/6.jpg "Configure Disqus")

#### 5. Comment and Moderation Settings

這邊可以設定你對留言的嚴謹度，可以自己選擇，我是選擇**Balanced**，如果未來很多垃圾留言，才會調整成比較嚴謹。

![Comment and Moderation Settings](/assets/images/post/2021-05-27-How-to-Add-third-comment-disqus-to-blog/7.jpg "Comment and Moderation Settings")

#### 6. 大功告成

結果如下圖，我覺得學習這類事情蠻有趣的，多吸收橫向知識，以後在規劃服務的時候，就有更多 Idea 可以提供，也不用一直重複造輪子，對未來挺有幫助的。

![Result!](/assets/images/post/2021-05-27-How-to-Add-third-comment-disqus-to-blog/8.jpg "Result!")
