---
title: Markdown 轉 BBCode 工具｜支援巴哈姆特發文格式
layout: splash
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
# Markdown 轉 BBCode 工具｜支援巴哈姆特發文格式

> 將常見的 Markdown 語法轉換為巴哈姆特支援的 BBCode 格式。支援標題、粗體、斜體、連結、圖片等基本語法，適合創作分享使用。

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
  <div style="flex: 1;">
    <textarea id="markdown" placeholder="請輸入 Markdown 內容..."></textarea>
      <div style="margin-top: 0.5rem; display: flex; gap: 0.5rem;">
        <button class="copy-button" style="background: #888;" onclick="loadExample()">🧪 載入範例</button>
        <button class="copy-button" style="background: #cc4444;" onclick="clearInput()">🧹 清除內容</button>
      </div>
  </div>
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

  // 標題處理
  bb = bb.replace(/^### (.*$)/gim, '[size=4][b]$1[/b][/size]');
  bb = bb.replace(/^## (.*$)/gim, '[size=5][b]$1[/b][/size]');
  bb = bb.replace(/^# (.*$)/gim, '[size=6][b]$1[/b][/size]');

  // 粗體、斜體、刪除線
  bb = bb.replace(/\*\*(.*?)\*\*/gim, '[b]$1[/b]');
  bb = bb.replace(/\*(.*?)\*/gim, '[i]$1[/i]');
  bb = bb.replace(/~~(.*?)~~/gim, '[s]$1[/s]');

  // 程式碼：用 quote 包覆
  bb = bb.replace(/```([\s\S]*?)```/g, '[quote]$1[/quote]');
  bb = bb.replace(/`(.*?)`/g, '[quote]$1[/quote]');

  // 圖片（巴哈格式）
  bb = bb.replace(/!\[(.*?)\]\((.*?)\)/gim, '[img=$2]');

  // 連結
  bb = bb.replace(/\[(.*?)\]\((.*?)\)/gim, '[url=$2]$1[/url]');

  // 巢狀清單處理
  bb = convertNestedLists(bb);

  // 移除多餘的 list 標籤
  bb = bb.replace(/\[\/ul\]\s*\[ul\]/g, '');
  bb = bb.replace(/\[\/ol\]\s*\[ol\]/g, '');

  // 清除多餘空行
  bb = bb.replace(/\n{3,}/g, '\n\n');

  return bb.trim();
}

// 將支援巢狀的 Markdown 清單轉換成對應的 BBCode 格式
function convertNestedLists(md) {
  const lines = md.split('\n'); // 將輸入內容按行拆開
  let bbcode = '';              // 最終輸出的 BBCode 結果
  const stack = [];             // 用來追蹤目前巢狀層級與 list 類型

  // 計算每行前面的縮排空格數，作為巢狀層級依據
  const getIndentLevel = (line) => line.match(/^(\s*)/)[1].length;

  lines.forEach((line) => {
    const trimmed = line.trim();          // 去除行首行尾空白
    const indent = getIndentLevel(line);  // 計算目前這行的縮排數

    // 判斷無序清單：- xxx
    const unorderedMatch = trimmed.match(/^[-*+] (.+)/);

    // 判斷有序清單：1. xxx
    const orderedMatch = trimmed.match(/^\d+\. (.+)/);

    let type = null;
    let content = '';

    // 判斷是無序還是有序，並提取內容
    if (unorderedMatch) {
      type = 'ul';
      content = unorderedMatch[1];
    } else if (orderedMatch) {
      type = 'ol';
      content = orderedMatch[1];
    } else {
      // 如果這行不是清單項目，結束所有清單標籤，回到正常段落處理
      while (stack.length > 0) {
        const tag = stack.pop();
        bbcode += `[/${tag.type}]\n`; // 關閉清單標籤
      }
      // 將當前行的原始文字加入 BBCode 字串並換行
      bbcode += line + '\n'; 
      return;
    }

    // 當前縮排比堆疊頂層小，表示需要關閉一層清單結構
    while (stack.length > 0 && indent < stack[stack.length - 1].indent) {
      const tag = stack.pop();
      bbcode += `[/${tag.type}]\n`;
    }

    // 如果當前行為新層級的清單，或清單類型改變，新增一層清單結構
    if (
      stack.length === 0 ||
      indent > stack[stack.length - 1].indent ||
      stack[stack.length - 1].type !== type
    ) {
      bbcode += `[${type}]\n`;
      stack.push({ type, indent });
    }

    // 加入實際清單內容
    bbcode += `[li]${content}[/li]\n`;
  });

  // 處理結尾時還殘留在 stack 中的清單，逐一關閉
  while (stack.length > 0) {
    const tag = stack.pop();
    bbcode += `[/${tag.type}]\n`;
  }

  return bbcode;
}

function copyBBCode() {
  bbOutput.select();
  document.execCommand("copy");
  alert("已複製 BBCode！");
}

function loadExample() {
  const exampleMarkdown = `
# 標題1
## 標題2
### 標題3

**粗體文字**
*斜體文字*
~~刪除線~~

\`單行程式碼\`
\`\`\`
多行程式碼
多行程式碼
\`\`\`

[Google](https://www.google.com)

![圖片](https://example.com/image.jpg)

- 無序清單項目 1
- 無序清單項目 2

- 巢狀清單項目
  - 更深層的清單項目
  
1. 有序清單項目 1
2. 有序清單項目 2
3. 巢狀有序清單項目
  1. 更深層的有序清單項目
  `;
  mdInput.value = exampleMarkdown;
  bbOutput.value = convertMarkdownToBBCode(exampleMarkdown);
}

function clearInput() {
  mdInput.value = '';
  bbOutput.value = '';
}
</script>

## ✅ 支援語法對照表（適用巴哈姆特）

| Markdown               | BBCode（轉換結果）                   | 備註                                     |
|------------------------|---------------------------------------|------------------------------------------|
| `# 標題`               | `[size=6][b]標題[/b][/size]`          | 用來模擬大標題                           |
| `**粗體**`             | `[b]粗體[/b]`                         |                                          |
| `*斜體*`               | `[i]斜體[/i]`                         |                                          |
| `~~刪除線~~`           | `[s]刪除線[/s]`                       |                                          |
| `` `程式碼` ``         | `[quote]程式碼[/quote]`               | 為避免 `[code]` 造成顯示問題             |
| ```` ```多行程式碼``` ```` | `[quote]多行程式碼[/quote]`         | 可跨行，貼文不易亂格式                   |
| `[名稱](網址)`         | `[url=網址]名稱[/url]`                |                                          |
| `![替代文字](圖片網址)` | `[img=圖片網址]`                      | 巴哈格式                                |
| `- 項目`               | `[ul][li]項目[/li][/ul]`              | 無序清單，建議包含在 `[ul]` 中           |
| `1. 項目`              | `[ol][li]項目[/li][/ol]`              | 有序清單，建議包含在 `[ol]` 中           |

---

### ⚠️ 注意事項

> 為避免貼文出現 &#91;code&#93; 等 HTML 編碼問題，本工具將原本的 [code] 語法改為使用 [quote] 顯示程式碼。如果你熟悉巴哈排版格式，也可自行將 [quote] 改回 [code] 使用。
> 
> 目前使用巢狀清單或縮排格式時，可能會產生多餘的空格或空行，建議貼上巴哈前手動檢查並刪除不必要的空格，以避免版面混亂。

---

