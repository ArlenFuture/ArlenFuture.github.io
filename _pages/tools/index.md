---
title: 小工具
layout: single
permalink: /tools/
classes: wide
comments: false
share: true

excerpt: 收錄實用工具，如 Markdown 轉 BBCode 工具、PNG 轉 WebP 批次處理、亂2 Online 盟徽 製作工具、亂2 Online 任務進度表等，幫助創作者與玩家更有效率地處理內容。

# SEO
title_meta: 創作工具箱｜Markdown、BBCode、PNG 轉 WebP、亂2 Online 盟徽製作、亂2 Online 任務進度表
description: 提供實用線上工具協助創作者與玩家，包括 Markdown → BBCode 轉換器、PNG → WebP 批次轉換器、亂2 Online 盟徽 製作工具、亂2 Online 任務進度表等，支援即時轉換、像素縮放、固定尺寸輸出。
canonical_url: https://arlenfuture.github.io/tools/
---

🧰 以下是我設計的一些小工具，讓你在創作、遊戲發表、社群貼文中更有效率：

<div class="tool-grid">

<h2>社群工具</h2>

<a class="tool-card" href="/tools/markdown-to-bbcode/">
  <h3>Markdown → BBCode</h3>
  <p>將 Markdown 語法即時轉換為巴哈姆特 BBCode，適合心得文、遊戲介紹、角色發表。</p>
  <span class="tool-tags">
    <span class="tag">文字處理</span>
    <span class="tag">巴哈姆特</span>
  </span>
</a>

<a class="tool-card" href="/tools/png-to-webp/">
  <h3>PNG → WebP + ZIP</h3>
  <p>批次將 PNG 圖片轉換為 WebP 格式並打包為 ZIP，支援進度條顯示，適合網站或遊戲圖片最佳化。</p>
  <span class="tool-tags">
    <span class="tag">圖片壓縮</span>
    <span class="tag">批次處理</span>
  </span>
</a>

<h2>遊戲工具</h2>

<a class="tool-card" href="/tools/ran2-badge-maker/">
  <h3>亂2 Online 盟徽 製作</h3>
  <p>為 亂2 Online 製作 16x11 的盟徽（Badge）圖片，支援圖片上傳編輯或空白畫布繪圖，輸出 BMP 格式。</p>
  <span class="tool-tags">
    <span class="tag">圖片編輯</span>
  </span>
</a>

<a class="tool-card" href="/tools/ran2-quests-tracker/">
  <h3>亂2 Online 任務進度</h3>
  <p>亂2 Online 任務進度追蹤清單，支援多角色進度、匯入匯出JSON檔。</p>
  <span class="tool-tags">
    <span class="tag">任務進度</span>
  </span>
</a>

<!-- 預留空間，未來擴充用 -->

</div>

<style>
.tool-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.2rem;
  margin-top: 1.5rem;
}
.tool-card {
  display: block;
  background: linear-gradient(135deg, #f8f9fa 0%, #ffffff 100%);
  padding: 1.2rem;
  border-radius: 12px;
  text-decoration: none;
  color: #333;
  border: 1px solid #e9ecef;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}
.tool-card:hover {
  box-shadow: 0 8px 25px rgba(0,0,0,0.12);
  transform: translateY(-2px);
  border-color: #76c7c0;
}
.tool-card:before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: linear-gradient(90deg, #76c7c0, #4fc3f7);
  opacity: 0;
  transition: opacity 0.3s ease;
}
.tool-card:hover:before {
  opacity: 1;
}
.tool-card h3 {
  margin-top: 0;
  margin-bottom: 0.6rem;
  font-size: 1.1rem;
  font-weight: 600;
}
.tool-card p {
  margin: 0 0 0.8rem 0;
  font-size: 0.95rem;
  line-height: 1.5;
  color: #666;
}
.tool-tags {
  display: flex;
  gap: 0.4rem;
  flex-wrap: wrap;
}
.tag {
  background: #e9ecef;
  color: #495057;
  padding: 0.2rem 0.5rem;
  border-radius: 12px;
  font-size: 0.8rem;
  font-weight: 500;
}
.tool-card:hover .tag {
  background: #76c7c0;
  color: white;
}
</style>