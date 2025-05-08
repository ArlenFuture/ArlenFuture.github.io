---
title: Markdown 轉 BBCode 工具｜支援巴哈姆特發文格式
layout: single
permalink: /tools/markdown-to-bbcode/
classes: wide
comments: false
share: true

# SEO 相關
excerpt: 線上工具可將 Markdown 語法轉換為 BBCode，方便在巴哈姆特發文，支援標題、粗體、斜體、連結、圖片等語法。
author_profile: false

# SEO meta
title_meta: Markdown 轉 BBCode 線上工具｜支援巴哈姆特發文格式
description: 將常見的 Markdown 語法（如粗體、圖片、連結）轉換為巴哈姆特支援的 BBCode，適合創作者發表作品、遊戲介紹、心得文使用。
canonical_url: https://arlenfuture.github.io/tools/markdown-to-bbcode/

---

> 將常見的 Markdown 語法轉換為巴哈姆特支援的 BBCode 格式。支援標題、粗體、斜體、連結、圖片等基本語法，適合創作分享使用。

## ✅ 支援語法對照表

| Markdown              | BBCode                         |
|-----------------------|--------------------------------|
| `# 標題`              | `[size=6][b]標題[/b][/size]`   |
| `**粗體**`            | `[b]粗體[/b]`                  |
| `*斜體*`              | `[i]斜體[/i]`                  |
| `~~刪除線~~`          | `[s]刪除線[/s]`                |
| `` `程式碼` ``        | `[code]程式碼[/code]`          |
| `[名稱](網址)`        | `[url=網址]名稱[/url]`         |
| `![替代文字](圖片網址)`| `[img]圖片網址[/img]`           |

---

## 🛠 Markdown → BBCode 工具

<style>
.markdown-bbcode-container {
  display: flex;
  flex-direction: row;
  gap: 1rem;
  margin-top: 1rem;
  flex-wrap: wrap;
}
.markdown-bbcode-container textarea {
  flex: 1;
  min-height: 300px;
  padding: 1rem;
  font-family: monospace;
  border: 1px solid #ccc;
  border-radius: 6px;
  resize: vertical;
  width: 100%;
  box-sizing: border-box;
}
@media screen and (max-width: 768px) {
  .markdown-bbcode-container {
    flex-direction: column;
  }
}
.copy-button {
  margin-top: 0.5rem;
  padding: 0.4rem 1rem;
  background: #0066cc;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}
.copy-button:hover {
  background: #004999;
}
</style>

<div class="markdown-bbcode-container">
  <textarea id="markdown" placeholder="請輸入 Markdown 內容..."></textarea>
  <div class="output" style="flex: 1;">
    <textarea id="bbcode" readonly placeholder="這裡會顯示 BBCode 結果..."></textarea>
    <button class="copy-button" onclick="copyBBCode()">📋 複製 BBCode</button>
  </div>
</div>

<script>
const mdInput = document.getElementById("markdown");
const bbOutput = document.getElementById("bbcode");

mdInput.addEventListener("input", () => {
  bbOutput.value = convertMarkdownToBBCode(mdInput.value);
});

function convertMarkdownToBBCode(md) {
  let bb = md;

  bb = bb.replace(/^### (.*$)/gim, '[size=4][b]$1[/b][/size]');
  bb = bb.replace(/^## (.*$)/gim, '[size=5][b]$1[/b][/size]');
  bb = bb.replace(/^# (.*$)/gim, '[size=6][b]$1[/b][/size]');

  bb = bb.replace(/\*\*(.*?)\*\*/gim, '[b]$1[/b]');
  bb = bb.replace(/\*(.*?)\*/gim, '[i]$1[/i]');
  bb = bb.replace(/~~(.*?)~~/gim, '[s]$1[/s]');
  bb = bb.replace(/`(.*?)`/gim, '[code]$1[/code]');

  bb = bb.replace(/!\[(.*?)\]\((.*?)\)/gim, '[img]$2[/img]');
  bb = bb.replace(/\[(.*?)\]\((.*?)\)/gim, '[url=$2]$1[/url]');

  bb = bb.replace(/\n{2,}/g, '\n\n');
  return bb.trim();
}

function copyBBCode() {
  bbOutput.select();
  document.execCommand("copy");
  alert("已複製 BBCode！");
}
</script>
