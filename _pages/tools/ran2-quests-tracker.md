---
title: 亂2 Online 任務進度表
layout: splash
permalink: /tools/ran2-quests-tracker/
classes: wide
comments: false
share: true
# SEO
excerpt: 亂2 Online 任務進度追蹤清單，支援多角色進度、匯入匯出JSON檔。
---

# 亂2 Online 任務進度表

> 可建立多角色存檔，自動保存進度，支援匯入/匯出備份。

> 請優先查看公車司機、虎令、監獄及人人任務的提示，這幾個任務有BUG、限制等級或戰力條件。

## 參考資料
- [巴哈姆特 不要有名字(gc10726) 攻略文章及 PDF](https://forum.gamer.com.tw/C.php?bsn=5270&snA=85329)

<style>
.quest-container {
  margin-top: 1em;
  border-left: 4px solid #ccc;
  padding-left: 1em;
}
.quest-list {
  list-style: none;
  padding: 0;
}
.quest-list li {
  margin: 0.5em 0;
}
.quest-list input[type="checkbox"] {
  transform: scale(1.2);
  margin-right: 0.5em;
}
#controls {
  margin: 1em 0;
}
#controls input, #controls button, #controls select {
  margin: 0.3em;
}
</style>

<div id="controls">
  <label>角色：
    <select id="profileSelect"></select>
  </label>
  <button id="newProfileBtn">建立角色</button>
  <button id="deleteProfileBtn">刪除角色</button>
  <br>
  <button id="exportBtn">匯出進度 (下載JSON)</button>
  <input type="file" id="importFile" accept=".json">
</div>

<h3>各校本館或學院</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q1">【劇情】新進學生介紹</li>
  <li><input type="checkbox" data-id="q2">【劇情】學院生註冊</li>
  <li><input type="checkbox" data-id="q3">【劇情】學生主任的測驗（技能點數+2）</li>
  <li><input type="checkbox" data-id="q4">【劇情】結界認證（技能點數+2）</li>
  <li><input type="checkbox" data-id="q5">【劇情】準備通過正門</li>
  <li><input type="checkbox" data-id="q6">【劇情】突如其來的研究論文（大於或等於190）</li>
  <li><input type="checkbox" data-id="q7">【劇情】異象調查</li>
  <li><input type="checkbox" data-id="q8">【劇情】定期測驗（聖門本館主任 能力點數+2）</li>
  <li><label>以下三校任務名稱不同</label></li>
  <li><input type="checkbox" data-id="q9">【劇情】戰爭的召喚(聖門)|【劇情】自我防衛(鳳凰)|【劇情】守護學院(玄嚴)（各校本館主任 能力點數+2）</li>
</ul>
</div>

</details>

<h3>聖門/玄嚴/鳳凰洞</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC: 公車司機</h4>
<blockquote>非常重要！一出校門請從公車司機一路解上去，千萬不要途中去跟物理老師對話！否則會無法接取物理老師的呼叫任務！</blockquote>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q12">【劇情】公車司機的請求(1)</li>
  <li><input type="checkbox" data-id="q13">【劇情】公車司機的請求(2)</li>
  <li><input type="checkbox" data-id="q14">【劇情】作業班長的請求</li>
  <li><input type="checkbox" data-id="q15">【劇情】物理老師的呼叫（技能點數+1）</li>
</ul>
</div>

<h4>NPC: 技術老師</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q16">【劇情】技術老師的測驗（技能點數+1）</li>
  </ul>
</div>

<h4>NPC: 物理老師</h4>
<blockquote>掃除炸彈、淨化公園 固定在聖門洞物理老師，其於任務在各學院洞對應的物理老師接取。</blockquote>
<div class="quest-container">
<ul class="quest-list">
  <li><label>以下三校任務名稱不同，玄嚴玩家有空再跟我回報任務名稱</label></li>
  <li><input type="checkbox" data-id="q17">【劇情】打倒冰凍可魯(聖門)|【劇情】淨化廢車場(鳳凰)|【劇情】掃除剪刀手(玄嚴)（技能點數+1）</li>
  <li><input type="checkbox" data-id="q18">【劇情】掃除炸彈（技能點數+1）</li>
  <li><input type="checkbox" data-id="q19">【劇情】淨化公園（技能點數+1）</li>
  <li><input type="checkbox" data-id="q20">【劇情】物理老師的考試</li>
  <li><input type="checkbox" data-id="q21">【劇情】紙幣認證（技能點數+1）</li>
  <li><input type="checkbox" data-id="q22">【劇情】發布命令書（技能點數+1）</li>
  <li><input type="checkbox" data-id="q23">【劇情】回收地圖（技能點數+1）</li>
  </ul>
</div>

<h4>NPC: 特遣人員</h4>
<blockquote>有綁技能點的任務，幾乎在外面就可以解，但如果想把全部任務解掉，120等以前進去是相對舒服的。</blockquote>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q24">【劇情】獲得特殊ID卡（技能點數+1）</li>
  <li><input type="checkbox" data-id="q25">【劇情】前往虎令學院地下2樓 (可不接)</li>
  <li><input type="checkbox" data-id="q26">【劇情】特遣人員的測驗</li>
  <li><input type="checkbox" data-id="q27">【劇情】特遣人員的請求（技能點數+1）</li>
</ul>
</div>

</details>


<h3>商洞</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC: 警察</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q28">【劇情】警察的委託（技能點數+1）</li>
  <li><input type="checkbox" data-id="q29">【劇情】調查實驗體（能力點數+1）</li>
  </ul>
</div>

<h4>NPC: 清潔工人</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q30">【劇情】鮮紅色的影子（技能點數+3，前置:深牢之怨）</li>
  <li><input type="checkbox" data-id="q31">【劇情】請求支援（技能點數+5）</li>
  <li><input type="checkbox" data-id="q32">【劇情】伏擊（技能點數+3，中洞 NPC: 典獄官）</li>
</ul>
</div>

<h4>NPC: 學院聯合戰隊隊長－亞恩</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q33">【劇情】深入死牢（能力點數+1，前置：斯利普議會長－議會的委託）</li>
  <li><input type="checkbox" data-id="q34">【劇情】實力的證明（火炎地獄鑰匙）</li>
  <li><input type="checkbox" data-id="q35">【劇情】更難突破的要塞 (火炎副本每日任務的前置) </li>
</ul>
</div>

<h4>NPC: 藍洛</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q36">【劇情】墮星之光（技能點數+10、能力點數+20）</li>
  <li><input type="checkbox" data-id="q37">【劇情】深淵的序曲（20 萬亂幣接取，前置：本洞 - 警察-謎樣的探險家）</li>
  <li><input type="checkbox" data-id="q38">【劇情】激戰前的測試（技能點數+7、綜合修練院-NPC:斯利普議會長）</li>
</ul>
</div>

<h4>NPC: 學院聯合戰隊隊員－凱特</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q39">【劇情】火焰的印記（能力點數+1）</li>
  <li><input type="checkbox" data-id="q40">【劇情】寒冰霸主的密令（能力點數+2）</li>
  <li><input type="checkbox" data-id="q41">【劇情】機械交響曲（能力點數+3）</li>
  <li><input type="checkbox" data-id="q42">【劇情】愛情解毒劑（能力點數+3）</li>
  <li><input type="checkbox" data-id="q43">【劇情】破壞之力（技能點數+8）</li>
  <li><input type="checkbox" data-id="q44">【劇情】預言家（技能點數+1，前置：激戰前的測試）</li>
  <li><input type="checkbox" data-id="q45">【劇情】古老的詛咒（技能點數+2，前置：預言家）</li>
</ul>
</div>

<h4>NPC: 紫宮遠</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q46">【劇情】聖財團機工館的治安問題(一)（技能點數+3、需轉奧義等級達到210等）</li>
  <li><input type="checkbox" data-id="q47">【劇情】聖財團機工館的治安問題(二)（技能點數+4、需轉奧義等級達到210等）</li>
</ul>
</div>

</details>

<h3>綜合碼頭</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC: 卡車司機</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q48">【劇情】回收卡車鑰匙</li>
  <li><input type="checkbox" data-id="q49">【劇情】汽油回收 </li>
  <li><input type="checkbox" data-id="q50">【劇情】去見老人（技能點數+3）</li>
</ul>
</div>

<h4>NPC: 可疑的老人</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q51">【劇情】老頭的禮物</li>
  <li><input type="checkbox" data-id="q52">【劇情】尋找文書</li>
  <li><input type="checkbox" data-id="q53">【劇情】確認淨水場水質</li>
  <li><input type="checkbox" data-id="q54">【劇情】修理發電機</li>
  <li><input type="checkbox" data-id="q55">【劇情】拿到青之秘密據點的帶子</li>
  <li><input type="checkbox" data-id="q56">【劇情】青之秘密據點帶子修復（技能點數+3）</li>
</ul>
</div>

<h4>NPC: 碼頭警察Ａ</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q57">【劇情】確認走私品</li>
  <li><input type="checkbox" data-id="q58">【劇情】逮捕走私犯</li>
  <li><input type="checkbox" data-id="q59">【劇情】調查建築物</li>
  <li><input type="checkbox" data-id="q60">【劇情】侵入「青」的秘密據點 </li>
  <li><input type="checkbox" data-id="q61">【劇情】搜索「青」的秘密據點 </li>
  <li><input type="checkbox" data-id="q62">【劇情】搜索「青」的秘密據點2樓</li>
  <li><input type="checkbox" data-id="q63">【劇情】搜索「青」的秘密據點3樓</li>
  <li><input type="checkbox" data-id="q64">【劇情】交回證據</li>
  <li><input type="checkbox" data-id="q65">【劇情】第一次考試（技能點數+2、能力點數+1、NPC：商洞－洪美蘭）</li>
  <li><input type="checkbox" data-id="q66">【劇情】第二次考試（技能點數+2、打冰凍小丑）</li>
  <li><input type="checkbox" data-id="q67">【劇情】第三次考試（獎勵:空間念珠[+7]、新手神裝別賣）</li>
</ul>
</div>

</details>

<h3>中洞</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC: 護士</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q68">【劇情】找尋遺物（技能點數+2）</li>
  <li><input type="checkbox" data-id="q69">【劇情】死亡領域（技能點數+4）</li>
  <li><input type="checkbox" data-id="q70">【劇情】尋找背包鑰匙（獎勵:時空斑指[+6]、新手神裝別賣）</li>
</ul>
</div>

</details>

<h3>聖財團私立監獄</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<blockquote>有戰力限制問題，越早解越好，200初不洗點的情況幾乎要脫掉全部裝備才能解。</blockquote>
<h4>NPC: 監獄警察</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q71">【劇情】確認信紙（技能點數+2）</li>
  <li><input type="checkbox" data-id="q72">【劇情】搜集珠子（技能點數+5）</li>
  <li><input type="checkbox" data-id="q73">【劇情】找尋嫌犯（能力點數+1，容易漏掉，監獄警察A 座標:51/105）</li>
</ul>
</div>

</details>

<h3>本洞</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC: 警察</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q74">【劇情】謎樣的探險家</li>
  <li><input type="checkbox" data-id="q75">【劇情】未知的動亂</li>
</ul>
</div>

<h4>NPC: 老頭</h4>
<blockquote>製作特殊戒指的獎勵，別丟商店，撐力量終身裝，賣了無法補救。</blockquote>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q76">【劇情】拾回舊書（技能點數+3）</li>
  <li><input type="checkbox" data-id="q77">【劇情】測試執行能力（能力點數+6）</li>
  <li><input type="checkbox" data-id="q78">【劇情】測試執行能力(2)（能力點數+9）</li>
  <li><input type="checkbox" data-id="q79">【劇情】測試執行能力(3)（能力點數+12）</li>
  <li><input type="checkbox" data-id="q80">【劇情】製作特殊戒指</li>
</ul>
</div>

<h4>NPC: 陽台</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q81">【劇情】鐵絲網上的小花（技能點數+4）</li>
</ul>
</div>

<h4>NPC: 神秘女子</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q82">【劇情】各學院地下圖書館調查（技能點數+2，需轉奧義等級260）</li>
  <li><input type="checkbox" data-id="q83">【劇情】集中營狀況調查（技能點數+5，需轉奧義等級260）</li>
</ul>
</div>

</details>

<h3>異界虎令本館 B3</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC: 虎令氣功部學生</h4>
<div class="quest-container"> 
<ul class="quest-list">
  <li><input type="checkbox" data-id="q84">【劇情】蒐集認證書材料（技能點數+2）</li>
  <li><input type="checkbox" data-id="q85">【劇情】我們的約定（技能點數+1、NPC：B1－虎令劍道部學生）</li>
  <li><input type="checkbox" data-id="q86">【劇情】血荒（技能點數+2、NPC：本館－崔基範）</li>
  <li><input type="checkbox" data-id="q87">【劇情】封印結界（技能點數+3、NPC：操場－江希珍）</li>
</ul>
</div>

</details>

<h3>異界虎令本館 B2</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC: 技術老師[虎令]</h4>
<div class="quest-container"> 
<ul class="quest-list">
  <li><input type="checkbox" data-id="q88">【劇情】蟲之血</li>
  <li><input type="checkbox" data-id="q89">【劇情】亡羊補牢（技能點數+2、NPC：B2－研究生）</li>
  <li><input type="checkbox" data-id="q90">【劇情】暴動的學生（前置：異象調查、NPC：本館－老師）</li>
  <li><input type="checkbox" data-id="q91">【劇情】暴動的真相（NPC：本館－老師）</li>
  <li><input type="checkbox" data-id="q92">【劇情】瘋狂的開端（技能點數+3、NPC：本館－老師）</li>
</ul>
</div>

</details>

<h3>異界虎令本館</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC: 轉學生</h4>
<div class="quest-container"> 
<ul class="quest-list">
  <li><input type="checkbox" data-id="q93">【劇情】成績單（技能點數+2，前置：異象調查）</li>
</ul>
</div>

</details>

<h3>綜合修練院</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC: 斯利普議會長</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q94">【劇情】議會的委託</li>
  <li><input type="checkbox" data-id="q95">【劇情】深牢之怨（技能點數+5，能力點數+1）</li>
</ul>
</div>

<h4>NPC: Dr.J</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q96">【劇情】失落的一段情</li>
  <li><input type="checkbox" data-id="q97">【劇情】秘密生化實驗（技能點數+3）</li>
</ul>
</div>

</details>

<h3>學院廣場</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC: 星辰守護者</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q98">【劇情】原罪之書的關聯（能力點數+3）</li>
</ul>
</div>

</details>

<h3>聖財團會議室</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC: 風紀官－彭文太</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q99">【劇情】發現青基地</li>
  <li><input type="checkbox" data-id="q100">【劇情】青基地的主事者（NPC：青基地A區3F－青基地角頭）</li>
  <li><input type="checkbox" data-id="q101">【劇情】來自青基地的援助（技能點數+1、NPC：陽光男孩）</li>
</ul>
</div>

</details>

<h3>赤鳳任務總整理</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC 位置</h4>
<blockquote>
<ul>
  <li>赤鳳城 (37/16)－小龍女</li>
  <li>赤鳳城 (30/30)－九方黎生</li>
  <li>赤鳳城 (34/1)－紅查斌</li>
  <li>赤鳳宮 (28/10)－殷平風</li>
  <li>赤鳳宮內殿 (40/6)－驚慌失措的小兵</li>
</ul>
</blockquote>

<h4>中藥任務 掉落怪物</h4>
<blockquote>
<ul>
  <li>透骨樑: 二刀 二劍 二弓</li>
  <li>仙鶴根: 二槍 二槌 二方 一刀</li>
  <li>紫花曼陀羅: 一刀 一劍 一弓</li>
  <li>松篸: 一弓 一鎚 一槍 一方</li>
  <li>碎米麩: 下級刺客</li>
</ul>
</blockquote>

<h4>任務小訣竅</h4>
<blockquote>
<ul>
  <li>赤鳳地圖內掉落的命運箱子必定是 恐龍 及 將軍系列怪 可以利用這個機制，先把將軍打出來，但不要打掉，後續任務需要時再打掉，節省時間。</li>
  <li>小龍女的消失 及 龍女憐香的煩惱 這兩個系列任務是有重疊的，遇到打怪可先解另一條，就不用打兩次。</li>
</ul>
</blockquote>

<h4>注意事項</h4>
<blockquote>赤鳳宮內殿，命中率要求稍高，可使用`魂武` 或者 `命中裝備`打過去，精神系可無視這條。</blockquote>

<h3>學院廣場</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC: 申元貞</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q102">【劇情】小龍女的消失（能力點數+1）</li>
  <li><input type="checkbox" data-id="q103">【劇情】追姬（能力點數+1）</li>
  <li><input type="checkbox" data-id="q104">【劇情】龍女憐香（能力點數+6）</li>
  <li><input type="checkbox" data-id="q105">【劇情】不遠的將來（能力點數+10）</li>
</ul>
</div>

</details>

<h3>赤鳳城</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC: 小龍女</h4>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q106">【劇情】龍女憐香的煩惱（技能點數+2）</li>
  <li><input type="checkbox" data-id="q107">【劇情】九方黎生的請求(1)（技能點數+5）</li>
  <li><input type="checkbox" data-id="q108">【劇情】蒼龍的未來（技能點數+8）</li>
  <li><input type="checkbox" data-id="q109">【劇情】九方黎生的請求(2)（技能點數+6）</li>
  <li><input type="checkbox" data-id="q110">【劇情】最後的機會（技能點數+9）</li>
  <li><input type="checkbox" data-id="q111">【劇情】混亂的始源</li>
</ul>
</div>

<h4>NPC: 九方黎生</h4>
<blockquote>等級達到270，且完成上述任務</blockquote>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q112">【劇情】九方黎生的請求(2)（技能點數+6）</li>
  <li><input type="checkbox" data-id="q113">【劇情】最後的機會（技能點數+9、NPC：赤鳳宮 (28/10)－殷平風）</li>
  <li><input type="checkbox" data-id="q114">【劇情】混亂的始源（NPC：赤鳳宮 (28/10)－殷平風）</li>
</ul>
</div>

</details>
</details>

<h3>摸魂</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<blockquote>撿完丟出來，不影響任務回報。</blockquote>

<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q115">【劇情】邪惡之源-善妒之女：提斯迪蒙娜之魂（技能點數+1）</li>
  <li><input type="checkbox" data-id="q116">【劇情】邪惡之源-猜忌之子：奧賽羅之魂（技能點數+1）</li>
  <li><input type="checkbox" data-id="q117">【劇情】學生會長的下落：虎令學生會長之魂（技能點數+1，高經驗重複任務前置）</li>
  <li><input type="checkbox" data-id="q118">【劇情】七原罪-妒忌之源：伊維厄斯之魂（技能點數+2）</li>  
  <li><input type="checkbox" data-id="q119">【劇情】火焰領主之魂</li>
  <li><input type="checkbox" data-id="q120">【劇情】寒霜領主之魂</li>
  <li><input type="checkbox" data-id="q121">【劇情】瘟疫領主之魂</li>
  <li><input type="checkbox" data-id="q122">【劇情】雷殛領主之魂</li>
  <li><input type="checkbox" data-id="q123">【劇情】元素吞噬者之魂</li>
</ul>
</div>

</details>

<h3>各學院門口及學院廣場</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<h4>NPC: 人人有功練</h4>
<blockquote>以下人人有功練任務必須要在限定等級內完成，否則任務自動消失。</blockquote>
<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q124">【劇情】惹事生非的街道 (100-120等)</li>
  <li><input type="checkbox" data-id="q124">【劇情】變態三男的逆襲 (110-130等)（技能點數+1 能力點數+1）</li>
  <li><input type="checkbox" data-id="q125">【劇情】賊頭殺殺殺 (120-140等)（技能點數+1 能力點數+1）</li>
  <li><input type="checkbox" data-id="q126">【劇情】怒殺野鴛鴦 (130-150等)（技能點數+1 能力點數+1）</li>
  <li><input type="checkbox" data-id="q127">【劇情】隱隱騷動之聲 (140-160等)（技能點數+1 能力點數+1）</li>
  <li><input type="checkbox" data-id="q128">【劇情】抑制噪音 (150-170等)（能力點數+4）</li>
  <li><input type="checkbox" data-id="q129">【劇情】探查異變 (160-180等)（技能點數+2 能力點數+3）</li>
  <li><input type="checkbox" data-id="q130">【劇情】詭異的異變人種 (170-190等)（技能點數+2 能力點數+3）</li>
  <li><input type="checkbox" data-id="q131">【劇情】阻止異變加劇 (180-200等)（技能點數+2 能力點數+3）</li>
  <li><input type="checkbox" data-id="q132">【劇情】異界虎令的毒惡深淵 (190-210等)（技能點數+2 能力點數+3）</li>
  <li><input type="checkbox" data-id="q133">【劇情】例行性訓練(1) (200-220等)（能力點數+3）</li>
  <li><input type="checkbox" data-id="q134">【劇情】例行性訓練(2) (210-230等)（技能點數+2）</li>
  <li><input type="checkbox" data-id="q135">【劇情】例行性訓練(3) (220-240等)（技能點數+2）</li>
  <li><input type="checkbox" data-id="q136">【劇情】例行性訓練(4) (230-250等)（技能點數+2）</li>
  <li><input type="checkbox" data-id="q137">【劇情】例行性訓練(5) (240-260等)（技能點數+2）</li>
  <li><input type="checkbox" data-id="q138">【劇情】歲月的痕跡 (250-270等)（技能點數+2）</li>
</ul>
</div>

</details>

<h3>轉職奧義流程</h3>

<details>
<summary style="cursor:pointer;">點此展開 / 收摺</summary>

<div class="quest-container">
<ul class="quest-list">
  <li><input type="checkbox" data-id="q139">【劇情】莫名的指責（NPC：商洞－紫宮遠）</li>
  <li><input type="checkbox" data-id="q140">【劇情】另一個自己（NPC：商洞－紫宮遠）</li>
  <li><input type="checkbox" data-id="q141">【劇情】災難的開始（NPC：本洞－神秘女子）</li>
</ul>
</div>

</details>

<script>
const STORAGE_KEY = 'ran2_quests_profiles';
let profiles = {};
let currentProfile = '';

function saveProfiles() {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(profiles));
}

function loadProfiles() {
  const data = localStorage.getItem(STORAGE_KEY);
  if (data) profiles = JSON.parse(data);
}

function refreshProfileList() {
  const sel = document.getElementById('profileSelect');
  sel.innerHTML = '';
  Object.keys(profiles).forEach(name => {
    const opt = document.createElement('option');
    opt.value = name;
    opt.textContent = name;
    sel.appendChild(opt);
  });
  if (currentProfile && profiles[currentProfile]) {
    sel.value = currentProfile;
  } else {
    currentProfile = sel.value || '';
  }
}

function loadProgress() {
  document.querySelectorAll('input[type="checkbox"]').forEach(cb => {
    const id = cb.dataset.id;
    cb.checked = profiles[currentProfile]?.[id] || false;
  });
}

function saveProgress() {
  if (!profiles[currentProfile]) profiles[currentProfile] = {};
  document.querySelectorAll('input[type="checkbox"]').forEach(cb => {
    const id = cb.dataset.id;
    profiles[currentProfile][id] = cb.checked;
  });
  saveProfiles();
}

document.addEventListener("DOMContentLoaded", function() {
  loadProfiles();
  if (!Object.keys(profiles).length) {
    profiles['預設角色'] = {};
  }
  currentProfile = Object.keys(profiles)[0];
  refreshProfileList();
  loadProgress();

  document.getElementById('profileSelect').addEventListener('change', e => {
    currentProfile = e.target.value;
    loadProgress();
  });

  document.getElementById('newProfileBtn').addEventListener('click', () => {
    const name = prompt('輸入新角色名稱:');
    if (name && !profiles[name]) {
      profiles[name] = {};
      currentProfile = name;
      saveProfiles();
      refreshProfileList();
      loadProgress();
    }
  });

  document.getElementById('deleteProfileBtn').addEventListener('click', () => {
    if (confirm(`確定要刪除角色 "${currentProfile}" 嗎？`)) {
      delete profiles[currentProfile];
      const names = Object.keys(profiles);
      currentProfile = names[0] || '';
      saveProfiles();
      refreshProfileList();
      loadProgress();
    }
  });

  document.querySelectorAll('input[type="checkbox"]').forEach(cb => {
    cb.addEventListener('change', saveProgress);
  });

  document.getElementById('exportBtn').addEventListener('click', () => {
    const data = JSON.stringify(profiles[currentProfile], null, 2);
    const blob = new Blob([data], { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const safeName = currentProfile ? currentProfile : 'default';
    const filename = safeName.replace(/[\\/:*?"<>|]/g, '_') + '-亂2任務進度表.json';
    const link = document.createElement('a');
    link.href = url;
    link.download = filename;
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
    URL.revokeObjectURL(url);
  });

  document.getElementById('importFile').addEventListener('change', (e) => {
    const file = e.target.files[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = function(event) {
      try {
        const obj = JSON.parse(event.target.result);
        profiles[currentProfile] = obj;
        saveProfiles();
        loadProgress();
        alert('匯入成功');
      } catch (err) {
        alert('匯入失敗：JSON格式錯誤');
      }
    };
    reader.readAsText(file);
  });
});
</script>
