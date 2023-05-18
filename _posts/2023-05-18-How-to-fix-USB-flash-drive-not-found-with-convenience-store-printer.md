---
title: "解決隨身碟在超商無法讀取到的問題【小知識】"
date: 2023-05-18T00:00:00+08:00
categories:
  - 小知識
tags:
  - 磁區分割
  - 超商列印
---
## 前言
最近去超商列印資料，發現一個有趣的情況，自己的隨身碟在自己電腦讀得到，但拿去超商卻獨不掉，嘗試格式化或者變換格式，卻沒有效果。

## 警告
以下操作會導致你的資料消失，請記得備份。

## 實際操作
以下是透過Windows去處理這個問題

### 開啟命令提示字元
~~~
Windows 標誌鍵 + R
~~~

或者直接搜尋命令提示字元或cmd皆可

### 開啟diskpart
~~~shell
diskpart
~~~
直接輸入以上指令

### 找到你要重新分割的裝置
~~~shell
list disk
~~~
直接輸入以上指令，並找到你的對應裝置記下編號。

### 指定你要重設的裝置
~~~shell
select disk {your_device_number}
~~~
輸入以上指令，並把```{your_device_number}```整段替換成你要重設的裝置編號。

範例
~~~shell
select disk 5
~~~

### 刪除所有分割區並重置硬碟
~~~shell
clean
~~~
這樣就大功告成啦! 剩下就走一般的格式化流程即可。

## 心得
雖然現在很多超商都有雲端資料上傳列印，但有些夾帶個資的資料，心裡還是毛毛的，所以有時候會想要透過實體USB去超商列印，這篇文章就給有遇到類似問題的人參考啦。

## 參考文章

- [使用Windows DiskPart重置SSD](https://www.crucial.tw/support/articles-faq-ssd/reset-ssd-with-windows-diskpart)