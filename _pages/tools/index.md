---
title: 小工具
layout: single
permalink: /tools/
classes: wide
comments: false
share: true

excerpt: 收錄實用工具，如 Markdown 轉 BBCode 工具、亂2 Online 盟徽裁切器等，幫助創作者與玩家更有效率地處理內容。

# SEO
title_meta: 創作工具箱｜Markdown、BBCode、亂2 Online 盟徽製作
description: 提供實用線上工具協助創作者與玩家，包括 Markdown → BBCode 轉換器、亂2 Online 盟徽裁切器等，支援即時轉換、像素縮放、固定尺寸輸出。
canonical_url: https://arlenfuture.github.io/tools/
---

🧰 以下是我設計的一些小工具，讓你在創作、遊戲發表、社群貼文中更有效率：

<div class="tool-grid">

<a class="tool-card" href="/tools/markdown-to-bbcode/">
  <h3>Markdown → BBCode 工具</h3>
  <p>將 Markdown 語法即時轉換為巴哈姆特 BBCode，適合心得文、遊戲介紹、角色發表。</p>
</a>

<a class="tool-card" href="/tools/ran2-badge-cropper/">
  <h3>亂2 Online 盟徽裁切器</h3>
  <p>為《亂2 Online》製作固定 16x11 的盟徽圖片，支援比例裁切與縮放演算法選擇。</p>
</a>

<!-- 預留空間，未來擴充用 -->

</div>

<style>
.tool-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}
.tool-card {
  display: block;
  background: #f8f8f8;
  padding: 1rem;
  border-radius: 10px;
  text-decoration: none;
  color: #333;
  border: 1px solid #e0e0e0;
  transition: box-shadow 0.2s ease;
}
.tool-card:hover {
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}
.tool-card h3 {
  margin-top: 0;
  margin-bottom: 0.4rem;
}
.tool-card p {
  margin: 0;
  font-size: 0.95rem;
}
</style>
