---
title: "【開發好好用 #1】在本機快速架設測試用SMTP伺服器"
date: 2021-05-25T00:00:00+08:00
categories:
  - 開發好好用
tags:
  - SMTP
  - .NET Core
  - C#
---

每次開發到 SMTP 相關應用，就會衍生一個問題，我要用什麼來測試，找人要 SMTP Server，人家可能不給你，用自己的 Gmail 去申請 SMTP Server 會把開發環境弄髒，自己透過 Windows 內建架設，版本可能不對，例如:家用版，而且還要事後跑設定刪除。那有沒有一個比較輕量的 SMTP Server 可以用，今天就是來推薦這個軟體，**smtp4dev**。

## 特色

- 免費
- 不用設定
- 刪除容易

## 程式下載

- [rnwood/smtp4dev](https://github.com/rnwood/smtp4dev)

## 範例程式

- [ArlenFuture/SmtpClient.Sample](https://github.com/ArlenFuture/SmtpClient.Sample)

## 文章環境

- OS : Win 10 20H2 Home Edition
- IDE : Visual Studio 2019

## 建置流程

### Step1. 建置測試用的 SmtpClient 程式

如果不想自己建置的話，可以直接透過上面的範例程式去做測試，但這邊還是會簡單提一下範例程式的架構跟邏輯。

範例程式是用`.NET 5`建立的`ASP.NET Core Web API`

SMTP Server Host 已經存在 appsetting.json 裡，有需要可以從這裡修改。

開起來畫面會像是這樣

![SmtpClient.Sample](/assets/images/post/2021-05-25-How-to-easy-test-your-smtp-client-on-local/1.jpg "SmtpClient.Sample")

點開後，可以從底下的 Request body 去傳入要發送的訊息。

![Request body](/assets/images/post/2021-05-25-How-to-easy-test-your-smtp-client-on-local/2.jpg "Request body")

現在按下去，會失敗，因為你 SMTP Server 還沒開 xD。

### Step2. 建置測試用 SMTP Server

我個人是使用**Rnwood.Smtp4dev-win-x64-3.1.3.2**這個版本的，請開啟以下這個檔案

```
Rnwood.Smtp4dev.exe
```

開啟後，畫面如下圖

![Smtp4dev](/assets/images/post/2021-05-25-How-to-easy-test-your-smtp-client-on-local/3.jpg "Smtp4dev")

紅圈是他前端視覺化的位置，如下圖

![Smtp4dev front end](/assets/images/post/2021-05-25-How-to-easy-test-your-smtp-client-on-local/4.jpg "Smtp4dev front end")

### Step3. 透過程式去發送 Message 給 SMTP Server

這邊就用範例程式去發送 Message

![Request body](/assets/images/post/2021-05-25-How-to-easy-test-your-smtp-client-on-local/2.jpg "Request body")

### Step4. 接收資料，大功告成!

回到**Smtp4dev**，就能看到剛剛的 Message 出現在這裡了!

而且不用時，直接刪除就可以，也沒有特別設定開發環境，真的方便很多。

![Smtp4dev Message](/assets/images/post/2021-05-25-How-to-easy-test-your-smtp-client-on-local/5.jpg "Smtp4dev Message")

## 參考

- [System.Net.Mail 命名空間](https://docs.microsoft.com/zh-tw/dotnet/api/system.net.mail?view=net-5.0)
- [rnwood/smtp4dev](https://github.com/rnwood/smtp4dev)
