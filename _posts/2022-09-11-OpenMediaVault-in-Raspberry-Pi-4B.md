---
title: "將你的樹梅派化身為個人NAS【樹梅派】"
date: 2022-09-11T00:00:00+08:00
categories:
  - 樹梅派
tags:
  - Raspberry Pi 4 Model B
  - Open Media Vault
---

這篇文章會分享關於在樹梅派上建置Open Media Vault的流程。

## 建置步驟

### Step1. 把系統寫到記憶卡內

我這邊選擇使用官方的**Raspberry Pi OS Lite(64-bit)**，並使用**Raspberry Pi Imager**把系統寫到記憶卡內。

P.S.因為發文時OpneMediaVault還沒有發布64位元樹梅派版本的映像檔，所以這邊選擇使用樹梅派官方的OS再另外安裝。

### Step2. 先對系統做完整更新

安裝更新
```shell
sudo apt update -y && sudo apt upgrade -y
```

清除安裝套件
```shell
sudo apt clean
```

### Step3. 執行安裝指令

安裝後會把SSH等登入方式重置，安裝時間約耗時10分鐘，跑完會重開機。

```shell
sudo wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash
```

### Step4. 取得裝置IP位置，建議使用有線網路。

等等要使用這組IP登入進OpenMediaVault的管理介面。

我個人是使用以下兩種方式去查詢。
1. 直接接螢幕確認IP，使用指令查詢IP。

```shell
ifconfig
```

2. 如果環境不允許接螢幕，可以從Router那邊去查詢，發送的IP。

### Step5. 透過IP位址登入進OpenMediaVault的網頁管理介面

~~~
http://ipaddress
~~~

以下是預設用戶名稱跟密碼，記得透過介面更改預設密碼。
~~~
Username: admin
Password: openmediavault
~~~
![更改預設密碼](/assets/images/post/2022-09-11-OpenMediaVault-in-Raspberry-Pi-4B/1.jpg "更改預設密碼")

### Step6. 更改連線方式只能透過SSL/TLS方式連線

此步驟非必要，單純安全考量。

#### 系統 -> 憑證 -> SSL
建立自己的自簽憑證

![建立自己的憑證](/assets/images/post/2022-09-11-OpenMediaVault-in-Raspberry-Pi-4B/2.jpg "建立自己的憑證")

#### 系統 -> 工作台
勾選以下選項，並選擇剛剛建立的憑證。
- SSL/TLS已啟用
- 強制SSL/TLS

![啟用SSL/TLS](/assets/images/post/2022-09-11-OpenMediaVault-in-Raspberry-Pi-4B/3.jpg "啟用SSL/TLS")

### Step7. 透過SSL/TLS連上網頁管理介面

~~~
https://ipaddress
~~~

### Step8. 檢查OpenMediaVault是否有需要更新

系統 -> 更新管理 -> 更新

### Step9. Done!

基本設定就到此為止了~

## 參考

- [OpenMediaVault-Plugin-Developers/installScript](https://github.com/OpenMediaVault-Plugin-Developers/installScript)
