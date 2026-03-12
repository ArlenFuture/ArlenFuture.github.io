---
title: 燕雲十六聲｜儲值計算機
permalink: /tools/wwm-recharge-comparator/
comments: false
share: true

excerpt: 比較 MyCard 折扣與 Google Play 點數回饋，計算燕雲十六聲哪種儲值方式更划算，支援信用卡回饋與外國手續費設定。

title_meta: 燕雲十六聲｜儲值計算機
canonical_url: https://arlenfuture.github.io/tools/wwm-recharge-comparator/
---

> 輸入消費金額與各項回饋條件，自動計算哪種儲值方式最划算。

> 本計算機結果僅供參考，實際優惠以各平台公告為準。

<style>
.calc-container {
    max-width: 720px;
    margin: auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
}

.calc-container input[type="checkbox"] {
    width: auto;
    padding: 0;
    margin-top: 0;
    vertical-align: middle;
}

.calc-container label:has(input[type="checkbox"]) {
    display: flex;
    align-items: center;
    gap: 8px;
    cursor: pointer;
}

.section {
    margin-top: 25px;
}

label {
    display: block;
    margin-top: 10px;
}

.calc-container input,
.calc-container select {
    width: 100%;
    padding: 8px;
    margin-top: 5px;
    box-sizing: border-box;
}

.calc-container button {
    margin-top: 20px;
    width: 100%;
    padding: 12px;
    font-size: 16px;
    background: #4CAF50;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

.calc-container button:hover {
    background: #45a049;
}

.result {
    margin-top: 20px;
    padding: 15px;
    background: #eef7ff;
    border-radius: 6px;
    line-height: 1.8;
}
</style>

<div class="calc-container">

<!-- 儲值建議圖 -->
<div style="text-align: center; margin-bottom: 20px;">
    <img src="/assets/images/post/tools/wwm-recharge-comparator/wwm-recharge-guide.jpg" 
         alt="燕雲十六聲儲值面額建議" 
         style="max-width: 100%; border-radius: 8px;">
    <p style="margin-top: 10px; font-size: 0.95rem; color: #555;">
        完成首儲獎勵後，黃色區塊的面額 CP 值最高，建議作為日常儲值的優先選擇。
    </p>
</div>

<div class="section">
    <h3>基本</h3>
    <label>消費金額</label>
    <input id="amount" type="number" value="315">
</div>

<div class="section">
    <h3>MyCard</h3>
    <label>MyCard 折數</label>
    <input id="mycardDiscount" type="number" step="0.01" value="0.95">
    <label>MyCard 信用卡回饋 (%)</label>
    <input id="mycardCredit" type="number" value="5">
</div>

<div class="section">
    <h3>Google Play</h3>
    <label>Play 等級</label>
    <select id="playLevel" onchange="updatePoints()">
        <option value="1">銅 (1)</option>
        <option value="1.25">銀 (1.25)</option>
        <option value="1.5" selected>黃金 (1.5)</option>
        <option value="1.75">白金 (1.75)</option>
        <option value="2">鑽石 (2)</option>
    </select>

    <label>每 $30 獲得點數</label>
    <input id="pointsPer30" type="number" step="0.01" value="1.5">

    <label>活動倍率</label>
    <input id="eventMultiplier" type="number" value="1">

    <label>點數兌換</label>
    <select id="pointValueSelect" onchange="updatePointValue()">
        <option value="0.3" selected>Google Play 抵用金 (0.3)</option>
    </select>
    <input id="pointValue" type="number" step="0.01" value="0.3" readonly>

    <label>Google Play 信用卡回饋 (%)</label>
    <input id="googleCredit" type="number" value="6">

    <label>
        <input type="checkbox" id="foreignFee">
        1.5% 外國交易手續費
    </label>
</div>

<button onclick="calculate()">計算</button>

<div class="result" id="result"></div>

</div>

<script>
function updatePoints() {
    let level = document.getElementById("playLevel").value;
    document.getElementById("pointsPer30").value = level;
}

function updatePointValue() {
    let value = document.getElementById("pointValueSelect").value;
    document.getElementById("pointValue").value = value;
}

function calculate() {
    const epsilon = 0.01;

    let amount = parseFloat(document.getElementById("amount").value);

    // MyCard
    let mycardDiscount = parseFloat(document.getElementById("mycardDiscount").value);
    let mycardCredit = parseFloat(document.getElementById("mycardCredit").value) / 100;
    let mycardCost = amount * mycardDiscount;
    let mycardReward = mycardCost * mycardCredit;
    let mycardFinal = mycardCost - mycardReward;

    // Google Play
    let pointsPer30 = parseFloat(document.getElementById("pointsPer30").value);
    let eventMultiplier = parseFloat(document.getElementById("eventMultiplier").value);
    let pointValue = parseFloat(document.getElementById("pointValue").value);
    let googleCredit = parseFloat(document.getElementById("googleCredit").value) / 100;
    let foreignFee = document.getElementById("foreignFee").checked ? 0.015 : 0;

    let actualCharge = amount * (1 + foreignFee);
    let googleReward = actualCharge * googleCredit;
    let basePoints = (amount / 30) * pointsPer30;
    let points = basePoints * eventMultiplier;
    let pointMoney = points * pointValue;
    let googleFinal = actualCharge - googleReward - pointMoney;

    let mycardFinalRound = Number(mycardFinal.toFixed(2));
    let googleFinalRound = Number(googleFinal.toFixed(2));
    let diff = Math.abs(mycardFinalRound - googleFinalRound).toFixed(2);

    let winner = "";
    let saveText = "";

    if (Math.abs(mycardFinalRound - googleFinalRound) < epsilon) {
        winner = "🤝 兩者成本幾乎相同";
        saveText = "差異小於 0.01";
    } else if (mycardFinalRound < googleFinalRound) {
        winner = "🏆 MyCard 比較划算";
        saveText = `多省下 ${diff}`;
    } else {
        winner = "🏆 Google Play 比較划算";
        saveText = `多省下 ${diff}`;
    }

    let neededMultiplier = (actualCharge - googleReward - mycardFinal) / (basePoints * pointValue);
    neededMultiplier = Math.max(0, Number(neededMultiplier.toFixed(2)));

    eventMultiplier = Number(eventMultiplier.toFixed(2));

    document.getElementById("result").innerHTML = `
MyCard 最終成本: ${mycardFinalRound}<br>
Google Play 最終成本: ${googleFinalRound}<br><br>
<b>${winner}</b><br>
${saveText}<br><br>
目前活動倍率: ${eventMultiplier}x<br>
打平或打贏 MyCard 需要倍率: ${neededMultiplier}x
    `;
}
</script>