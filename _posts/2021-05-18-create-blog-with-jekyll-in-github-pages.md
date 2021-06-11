---
title: "【架設部落格 #1】利用Jekyll在Github Pages上免費架設個人部落格"
date: 2021-05-18T16:20:02+08:00
categories:
  - 從零開始架設部落格
tags:
  - Jekyll
  - Github Pages
  - Minimal Mistakes
  - blog
---

前陣子一直想找個地方去整理自己的筆記，原本人選 Blogspot，但研究了一陣子發現不是很符合自己的需求，所以為自己整理出以下幾個重點，一定要符合，才會去選擇。

- 免費
- 版本控制
- 文章好轉移
- 分類清楚

架設在 Github Pages 上，版本控制跟費用問題一次搞定，雖然免費，但有流量限制及靜態頁面的限制，預設的 Jekyll 有支援 Markdown 去撰寫所以文章轉移也解決了。分類的問題，我選擇了 Minimal Mistakes，預設就有標籤及分類的功能，版型也比 Github 預設的好看許多。

## 環境安裝

我文章用的環境是 Windows 10 20H2，理論上 Mac、Linux 都可以做操作。

### 預先安裝或申請

- [Github Account](https://github.com/)
- [Jekyll Installation](https://jekyllrb.com/docs/installation/)

### 文章內帶著你做

- [Minimal Mistakes Quick-Start Guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#gem-based-method)

## 建置流程

### Step1. 從 Minimal Mistakes remote theme starter 複製一份到你的 Github repository

- [Minimal Mistakes remote theme starter](https://github.com/mmistakes/mm-github-pages-starter/generate)

![Fork repository](/assets/images/post/2021-05-18-create-blog-with-jekyll-in-github-pages/1.jpg "Fork repository")

1. 記得**Repository name**要按照格式寫`UserName.github.io`，`UserName`記得替換成自己的，以我來說就是換成`ArlenFuture`全名是`ArlenFuture.github.io`。
2. 不是商業版的都一律設定成**Public**外部才看的到
3. 按下去過幾一段時間，就能在`https://UserName.github.io/`看到啦，一樣`UserName`替換成自己的。

### Step2. 修改\_config.yml 將內容修改成自己的

這時你會在你的 Github repository 看到你剛剛建立的專案，此時用版本控制把專案 Clone 下來，修改
`_config.yml`，把裡面的參數設定成自己的。

### Step3. 測試在本機預覽 Jekyll 專案

首先進入 CMD

```
jekyll -v
```

看一下版本資訊，基本上就確定它的安裝

![jekyll version](/assets/images/post/2021-05-18-create-blog-with-jekyll-in-github-pages/2.jpg "jekyll version")

1. 這時到你 Clone 專案的地方下這個指令安裝套件

```
bundle install
```

2. 執行這段把專案跑起來

```
bundle exec jekyll serve
```

如果出現像是下面這樣的問題

![bundle exec jekyll serve error](/assets/images/post/2021-05-18-create-blog-with-jekyll-in-github-pages/3.jpg "bundle exec jekyll serve error")

去\_config.yml 加入這個參數一樣`UserName`替換成自己的。

```
repository: UserName/UserName.github.io
```

像是下圖

![add repository name for build](/assets/images/post/2021-05-18-create-blog-with-jekyll-in-github-pages/4.jpg "add repository name for build")

接著就可以順利執行這個網站啦

![Hello World!](/assets/images/post/2021-05-18-create-blog-with-jekyll-in-github-pages/5.jpg "Hello World!")

### Step3. 刪掉原本\_post 內的文件

### Step4. 將專案透過版控 Push 到 Github

大功告成!!
