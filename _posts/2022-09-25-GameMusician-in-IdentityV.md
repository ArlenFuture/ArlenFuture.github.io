---
title: "我為第五人格PC版寫了一個自動演奏軟體【軟體開發】"
header:
  teaser: "/assets/images/post/2022-09-25-GameMusician-in-IdentityV/teaser.jpg"
date: 2022-09-25T00:00:00+08:00
categories:
  - 軟體開發
tags:
  - .NET
  - MIDI
  - 第五人格
---
## 前言
前陣子第五人格更新演奏傢俱的功能，讓我也想體驗一下，但可惜本人是音癡xD，不識五線譜那種，所以我的RD魂就被點燃了，這篇文章會聊聊設計原因及技術選型之類的。

## 敘述
遊戲演奏家是一款能在第五人格PC端自動彈琴的程式。
目前有的功能
- Midi檔讀取
- 自動演奏

***目前程式還在初期階段。***
## 預覽
![程式預覽](/assets/images/post/2022-09-25-GameMusician-in-IdentityV/teaser.jpg "程式預覽")

## Demo
[![【第五人格：鋼琴演奏】吉諾佩第 第一號 Gymnopédie No.1 【阿冷】|【アイデンティティⅤ】【IdentityV】](https://img.youtube.com/vi/2SgY3JhA210/0.jpg)](https://www.youtube.com/watch?v=2SgY3JhA210)

## 實作原理
- 為什麼選擇MIDI檔?
```
主要是因為我希望能使用既有的數位音樂資料，這樣我就不用自己造輪子，建立自己的格式，也能使用原有社群力量。
```
- 音高是如何分類?
```
目前初期的版本是取得Middle C的部分去做三分法，剛好應對到第五人格的三個音高。
```
- 主要流程
```
讀取MIDI -> 解析樂譜 -> 轉換成按鍵 -> 模擬鍵盤輸入
```

## 技術選型
- .NET 6
- [InputManaer](https://www.codeproject.com/Articles/117657/InputManager-library-Track-user-input-and-simulate)
- [DryWetMIDI](https://github.com/melanchall/drywetmidi)

RD魂就是想要用最新的技術xD

## 知識
- 為什麼要UAC權限?
```
因為要模擬驅動層級的鍵盤，需要足夠的權限，才有辦法在第五人格的視窗內，模擬鍵盤輸出。
```
- 為什麼檔案容量有點大?
```
因為我猜多數使用者環境下不會有.NET 6，為了減少問題我就將Lib包進去了。
```
- 第五人格演奏是基於C大調去運作的。

## 未來展望
以下是我認為這隻程式未來也許可以加入的功能
- 分離不同音軌，將鋼琴的部分，單獨抽離演奏。
- 將樂譜自動轉換成C大調。
- 新增玉蕭的演奏的功能(音高只有兩階)。
- 介面友善化，轉換成可以有播放清單之類的功能。

## 如何使用?
1. 選擇你要播放的Midi檔
2. 停在第五人格的視窗
3. 按下Ctrl+F5去播放或暫停

## 已知問題
- 快速的切換播放中歌曲時，會有錯誤產生。

## 下載
https://github.com/ArlenFuture/GameMusician/releases/tag/v0.1.0-alpha

下載裡面的Release.zip即可。

## 專案位置
https://github.com/ArlenFuture/GameMusician

## 閒聊
其實程式大概在一週前，就差不多到這個完成度，但最近手上事情有點多，就先把程式開源出來，讓有興趣的人先體驗一下xD

不管是開發者或使用者，也歡迎在底下留言，讓我知道你對這程式有興趣xD 加快程式改版進度~