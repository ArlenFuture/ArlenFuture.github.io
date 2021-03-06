---
title: "提升影片流暢度，在A卡上開啟Fluid Motion【影片好好看】"
date: 2021-05-23T00:00:00+08:00
categories:
  - 影片好好看
tags:
  - AMD
  - Fluid Motion
  - Bluesky Frame Rate Converter
  - Potplayer
---

先簡單跟各位聊聊 Fluid Motion，這個技術主要是把原生 24 幀或 30 幀的影片透過演算法的方式補幀到 60 幀，藉此來提升影片流暢度，這篇會教你如何在 A 卡上開啟 Fluid Motion，並套用在 Potplayer 上面。

## 特色

- 免費
- 設定簡單

## 環境限制

AMD GCN1.0 以上的顯示卡 粗略估計(HD7750->Radeon VII)
只要在這範圍內的顯示卡都有支援
筆電的話，APU 也有支援，例如:R3、R5、R7-2X00U、H->R3、R5、R7-5X00U、H。

## 預先安裝

- [AMD 顯示卡驅動](https://www.amd.com/zh-hant/support)
- [Bluesky Frame Rate Converter](https://bluesky-soft.com/en/BlueskyFRC.html)
- [Potplayer](https://potplayer.daum.net/)

## 文章環境

![Hardware and AMD Driver version](/assets/images/post/2021-05-23-Enable-Fluid-motion-with-your-AMD-Card/1.jpg "Hardware and AMD Driver version")

![Bluesky Frame Rate Converter](/assets/images/post/2021-05-23-Enable-Fluid-motion-with-your-AMD-Card/2.jpg "Bluesky Frame Rate Converter")

## 建置流程

### Step1. Bluesky Frame Rate Converter 開啟 Fluid Motion

**Enable AMD Fluid Motion Video**這項目必開，其他的例如 AFM Mode 可以自己選擇，當 24->60 時，Mode1 的話，會用兩張原始的幀加三張插值去補幀，Mode2 的話，會用一張原始的幀加四張插值去補幀，簡單來說，就是二去運算的地方比較多，可能會比較流暢，但也有比較多瑕疵的可能，所以可以實際上看影片在做選擇，我平常預設是調 2，調 Auto，感覺常常有放棄補幀的情況。

![Bluesky Frame Rate Converter Setting](/assets/images/post/2021-05-23-Enable-Fluid-motion-with-your-AMD-Card/3.jpg "Bluesky Frame Rate Converter Setting")

### Step2. AMD Driver 開啟 Fluid Motion

以這張卡或者筆電 APU 來說畫面上不會顯示 Fluid Motion，所以這邊不用調整，會顯示的卡，例如:RX4X0、RX5X0 等等，就要記得把選項勾起來。

![AMD Driver Setting](/assets/images/post/2021-05-23-Enable-Fluid-motion-with-your-AMD-Card/4.jpg "AMD Driver Setting")

### Step3. Potplay 加入 Bluesky 濾鏡支援

在 Potplay 畫面點
右鍵 -> 濾鏡 -> 濾鏡/解碼器管理... -> 新增外部濾鏡 -> 路徑選擇
看你的播放器安裝的是什麼版本

64 位元

```
C:\Program Files\Bluesky Frame Rate Converter\BlueskyFRC64.dll
```

32 位元

```
C:\Program Files\Bluesky Frame Rate Converter\BlueskyFRC32.dll
```

-> 選 Bluesky Frame Rate Converter -> 優先順序改成**強制使用**

![Potplayer Setting](/assets/images/post/2021-05-23-Enable-Fluid-motion-with-your-AMD-Card/5.jpg "Potplayer Setting")
![Potplayer Setting](/assets/images/post/2021-05-23-Enable-Fluid-motion-with-your-AMD-Card/6.jpg "Potplayer Setting")

### Step4. 大功告成

輸出的 FPS 會在 60 附近浮動，剩下的就自己去感受吧。

示範影片

- [【日語】關於我轉生變成史萊姆這檔事 第 01 話【暴風龍維爾德拉】｜ Muse 木棉花 動畫 線上看](https://www.youtube.com/watch?v=gv8fwwHwqJQ&ab_channel=Muse%E6%9C%A8%E6%A3%89%E8%8A%B1-TW)

![示範影片](/assets/images/post/2021-05-23-Enable-Fluid-motion-with-your-AMD-Card/7.jpg "示範影片")
