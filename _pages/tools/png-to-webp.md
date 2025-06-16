---
title: PNG → WebP + ZIP 線上工具
layout: splash
permalink: /tools/png-to-webp/
classes: wide
comments: false
share: true
# SEO 相關
excerpt: 將多張 PNG 圖片轉換為 WebP 並打包為 ZIP，一鍵下載，支援進度條顯示，適合圖片批次壓縮使用。
author_profile: false
# SEO meta
title_meta: PNG → WebP + ZIP 線上工具
description: 線上工具可將多張 PNG 圖片轉為 WebP 格式並自動打包為 ZIP，支援進度條顯示與一鍵下載。
canonical_url: https://arlenfuture.github.io/tools/png-to-webp/
---

# PNG → WebP + ZIP 線上工具

> 將多張 PNG 圖片轉換為 WebP 格式，並自動打包成 ZIP 檔案下載，支援即時進度條顯示，適合批次壓縮、上傳前最佳化圖片。

<style>
#progressContainer {
    width: 100%;
    background-color: #e0e0e0;
    border-radius: 5px;
    margin-top: 20px;
    height: 20px;
}
#progressBar {
    width: 0%;
    height: 100%;
    background-color: #76c7c0;
    border-radius: 5px;
    text-align: center;
    color: white;
    line-height: 20px;
}
</style>

<input type="file" id="fileInput" accept="image/png" multiple>
<button id="convertBtn">轉換並下載 ZIP</button>
<div id="progressContainer">
    <div id="progressBar">0%</div>
</div>
<div id="output"></div>

<script src="https://cdn.jsdelivr.net/npm/jszip@3.10.1/dist/jszip.min.js" 
        integrity="sha256-rMfkFFWoB2W1/Zx+4bgHim0WC7vKRVrq6FTeZclH1Z4=" 
        crossorigin="anonymous"></script>
<script>
// 檢查 JSZip 是否正確載入
if (typeof JSZip === 'undefined') {
    alert('JSZip 庫載入失敗，請檢查網路連線或刷新頁面');
    throw new Error('JSZip library failed to load');
}

// 監聽檔案選擇變化，清除之前的結果
document.getElementById('fileInput').addEventListener('change', () => {
    const output = document.getElementById('output');
    const progressBar = document.getElementById('progressBar');
    
    // 清除之前的下載連結和進度
    output.innerHTML = '';
    progressBar.style.width = '0%';
    progressBar.textContent = '0%';
    progressBar.style.backgroundColor = '#76c7c0'; // 重置進度條顏色
});

document.getElementById('convertBtn').addEventListener('click', async () => {
    const files = document.getElementById('fileInput').files;
    if (files.length === 0) {
        alert('請選擇至少一個 PNG 檔案');
        return;
    }

    const zip = new JSZip(); // 建立 JSZip 實例
    const output = document.getElementById('output');
    const progressBar = document.getElementById('progressBar');
    const convertBtn = document.getElementById('convertBtn');
    
    // 清空輸出區域並禁用按鈕
    output.innerHTML = '';
    progressBar.style.width = '0%';
    progressBar.textContent = '0%';
    convertBtn.disabled = true;
    convertBtn.textContent = '轉換中...';

    try {
        for (let i = 0; i < files.length; i++) {
            const file = files[i];
            if (!file.type.startsWith('image/png')) {
                console.warn(`檔案 ${file.name} 不是 PNG 格式，跳過處理`);
                continue;
            }

            const img = new Image();
            const url = URL.createObjectURL(file);

            img.src = url;
            await img.decode();

            const canvas = document.createElement('canvas');
            canvas.width = img.width;
            canvas.height = img.height;

            const ctx = canvas.getContext('2d');
            ctx.drawImage(img, 0, 0);

            // 使用最高品質轉換為 WebP
            const blob = await new Promise(resolve => 
                canvas.toBlob(resolve, 'image/webp', 1.0)
            );

            if (!blob) {
                throw new Error(`無法轉換檔案 ${file.name}`);
            }

            // 讀取 Blob 並新增到 ZIP 中
            const webpName = file.name.replace(/\.png$/i, '.webp');
            const arrayBuffer = await blob.arrayBuffer();
            zip.file(webpName, arrayBuffer);

            URL.revokeObjectURL(url); // 釋放物件 URL

            // 更新進度條
            const progress = Math.round(((i + 1) / files.length) * 100);
            progressBar.style.width = `${progress}%`;
            progressBar.textContent = `${progress}%`;
        }

        // 生成 ZIP 並下載
        const zipBlob = await zip.generateAsync({ type: 'blob' });
        
        // 產生台灣時間戳記 (UTC+8)
        const now = new Date();
        const taiwanTime = new Date(now.getTime() + (8 * 60 * 60 * 1000));
        const timestamp = taiwanTime.toISOString().slice(0,19).replace(/:/g,'-');
        
        const zipLink = document.createElement('a');
        zipLink.href = URL.createObjectURL(zipBlob);
        zipLink.download = `webp_files_${timestamp}.zip`;
        zipLink.textContent = '點此下載 ZIP 檔案';
        zipLink.style.cssText = 'display: inline-block; padding: 10px 20px; background: #76c7c0; color: white; text-decoration: none; border-radius: 5px; margin-top: 10px;';
        output.appendChild(zipLink);

        // 完成後將進度條設為 100%
        progressBar.style.width = '100%';
        progressBar.textContent = '完成！';
        
    } catch (error) {
        console.error('轉換過程發生錯誤:', error);
        alert(`轉換失敗: ${error.message}`);
        progressBar.style.width = '0%';
        progressBar.textContent = '錯誤';
        progressBar.style.backgroundColor = '#ff6b6b';
    } finally {
        // 重新啟用按鈕
        convertBtn.disabled = false;
        convertBtn.textContent = '轉換並下載 ZIP';
    }
});
</script>