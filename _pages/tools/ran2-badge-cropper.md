---
title: 亂2 Online 盟徽 製作工具｜16x11 裁切器
layout: splash
permalink: /tools/ran2-badge-cropper/
comments: false
share: true

# SEO 相關
excerpt: 為 亂2 Online 製作 16x11 的盟徽（Badge）圖片，支援固定比例裁切、不同縮放演算法與 BMP 匯出。
author_profile: false

# SEO meta
title_meta: 圖片裁切工具｜16:11 裁切輸出 16x11 BMP
canonical_url: https://arlenfuture.github.io/tools/ran2-badge-cropper/
---

# 亂2 Online 盟徽 製作工具｜16x11 裁切器

> 拖曳選取圖片區塊，自動維持 16:11 比例，輸出固定大小 BMP。支援三種縮放演算法選擇，適合處理像素圖或高畫質圖片。

> 將輸出的 BMP 檔案儲存到以下位置：
> - C:\Users\使用者名稱\Documents
> - 或者直接在 Windows 11 中點擊「文件」資料夾。

<style>
#canvas-container {
  position: relative;
  max-width: 100%;
  margin: 1rem 0;
}
canvas, #crop-area {
  max-width: 100%;
  touch-action: none;
}
#crop-area {
  position: absolute;
  border: 2px dashed #f00;
  resize: both;
  overflow: hidden;
}
.toolbox {
  margin: 1rem 0;
}
</style>

<div class="toolbox">
  <input type="file" id="fileInput" accept="image/*">
  <label for="scaleType">縮放演算法：</label>
  <select id="scaleType">
    <option value="nearest">最近鄰 (Nearest)</option>
    <option value="bilinear">雙線性 (Bilinear)</option>
    <option value="bicubic">模擬雙三次 (Bicubic)</option>
  </select>
  <button onclick="exportImage()">📥 匯出 16x11 BMP</button>
</div>

<div id="canvas-container">
  <canvas id="sourceCanvas"></canvas>
  <div id="crop-area"></div>
</div>

<div style="margin-top: 1rem;">
  <strong>預覽：</strong>
  <br>
  <img id="previewImage" width="160" height="110" style="image-rendering: pixelated; border: 1px solid #ccc;">
</div>

<script>
const fileInput = document.getElementById("fileInput");
const canvas = document.getElementById("sourceCanvas");
const ctx = canvas.getContext("2d");
const cropArea = document.getElementById("crop-area");
const scaleType = document.getElementById("scaleType");
const previewImage = document.getElementById("previewImage");
let img = null;

fileInput.addEventListener("change", (e) => {
  const file = e.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = function(evt) {
    img = new Image();
    img.onload = () => {
      canvas.width = img.width;
      canvas.height = img.height;
      ctx.drawImage(img, 0, 0);
      cropArea.style.width = "160px";
      cropArea.style.height = "110px";
      cropArea.style.left = "10px";
      cropArea.style.top = "10px";
      updatePreview();
    }
    img.src = evt.target.result;
  }
  reader.readAsDataURL(file);
});

// 拖曳裁切框，限制範圍
let isDragging = false;
let dragOffsetX, dragOffsetY;

cropArea.addEventListener("mousedown", (e) => {
  if (e.target === cropArea) {
    isDragging = true;
    dragOffsetX = e.offsetX;
    dragOffsetY = e.offsetY;
  }
});
document.addEventListener("mouseup", () => {
  if (isDragging) updatePreview();
  isDragging = false;
});
document.addEventListener("mousemove", (e) => {
  if (!isDragging) return;
  const rect = canvas.getBoundingClientRect();
  const cropRect = cropArea.getBoundingClientRect();
  const containerRect = document.getElementById("canvas-container").getBoundingClientRect();

  let newLeft = e.clientX - rect.left - dragOffsetX;
  let newTop = e.clientY - rect.top - dragOffsetY;

  const maxLeft = canvas.width - cropArea.offsetWidth;
  const maxTop = canvas.height - cropArea.offsetHeight;

  newLeft = Math.max(0, Math.min(newLeft, canvas.width - cropArea.offsetWidth));
  newTop = Math.max(0, Math.min(newTop, canvas.height - cropArea.offsetHeight));

  cropArea.style.left = `${newLeft}px`;
  cropArea.style.top = `${newTop}px`;
});

// 調整大小，維持比例與限制範圍
new ResizeObserver(() => {
  const width = cropArea.offsetWidth;
  const newHeight = Math.round(width * 11 / 16);
  cropArea.style.height = `${newHeight}px`;

  // 限制不要超出 canvas
  const left = cropArea.offsetLeft;
  const top = cropArea.offsetTop;
  const maxWidth = canvas.width - left;
  const maxHeight = canvas.height - top;

  if (width > maxWidth) {
    cropArea.style.width = `${maxWidth}px`;
    cropArea.style.height = `${Math.round(maxWidth * 11 / 16)}px`;
  }
  if (newHeight > maxHeight) {
    const limitedHeight = maxHeight;
    const limitedWidth = Math.round(limitedHeight * 16 / 11);
    cropArea.style.height = `${limitedHeight}px`;
    cropArea.style.width = `${limitedWidth}px`;
  }

  updatePreview();
}).observe(cropArea);

// 預覽更新
function updatePreview() {
  if (!img) return;
  const rect = cropArea.getBoundingClientRect();
  const canvasRect = canvas.getBoundingClientRect();
  const scaleX = img.width / canvasRect.width;
  const scaleY = img.height / canvasRect.height;
  const sx = (rect.left - canvasRect.left) * scaleX;
  const sy = (rect.top - canvasRect.top) * scaleY;
  const sw = cropArea.offsetWidth * scaleX;
  const sh = cropArea.offsetHeight * scaleY;

  const output = document.createElement("canvas");
  output.width = 16;
  output.height = 11;
  const outCtx = output.getContext("2d");

  if (scaleType.value === "nearest") {
    outCtx.imageSmoothingEnabled = false;
    outCtx.drawImage(canvas, sx, sy, sw, sh, 0, 0, 16, 11);
  } else if (scaleType.value === "bilinear") {
    drawBilinear(canvas, sx, sy, sw, sh, output, 16, 11);
  } else {
    drawBicubic(canvas, sx, sy, sw, sh, output, 16, 11);
  }

  previewImage.src = output.toDataURL();
}

// 匯出下載 BMP 格式
function exportImage() {
  if (!previewImage.src) return alert("請先上傳圖片並裁切");

  // 建立一個新的 canvas 將 previewImage 畫上去
  const outputCanvas = document.createElement("canvas");
  outputCanvas.width = 16;
  outputCanvas.height = 11;
  const outCtx = outputCanvas.getContext("2d");

  const tempImage = new Image();
  tempImage.onload = function () {
    outCtx.drawImage(tempImage, 0, 0, 16, 11);
    outputCanvas.toBlob((blob) => {
      const link = document.createElement("a");
      link.download = "output.bmp";  // 確保為 .bmp
      link.href = URL.createObjectURL(blob);
      link.click();
    }, "image/bmp");
  };
  tempImage.src = previewImage.src;
}


// 補充演算法
function drawBilinear(source, sx, sy, sw, sh, destCanvas, dw, dh) {
  const src = source.getContext("2d").getImageData(sx, sy, sw, sh);
  const dest = destCanvas.getContext("2d");
  const out = dest.createImageData(dw, dh);
  for (let y = 0; y < dh; y++) {
    for (let x = 0; x < dw; x++) {
      const gx = x / dw * (sw - 1);
      const gy = y / dh * (sh - 1);
      const x0 = Math.floor(gx), y0 = Math.floor(gy);
      const x1 = Math.min(x0 + 1, sw - 1);
      const y1 = Math.min(y0 + 1, sh - 1);
      const dx = gx - x0;
      const dy = gy - y0;
      const c00 = getRGBA(src, x0, y0);
      const c10 = getRGBA(src, x1, y0);
      const c01 = getRGBA(src, x0, y1);
      const c11 = getRGBA(src, x1, y1);
      const c = c00.map((_, i) =>
        (1 - dx) * (1 - dy) * c00[i] +
        dx * (1 - dy) * c10[i] +
        (1 - dx) * dy * c01[i] +
        dx * dy * c11[i]
      );
      setRGBA(out, x, y, c);
    }
  }
  dest.putImageData(out, 0, 0);
}

function drawBicubic(source, sx, sy, sw, sh, destCanvas, dw, dh) {
  const src = source.getContext("2d").getImageData(sx, sy, sw, sh);
  const dest = destCanvas.getContext("2d");
  const out = dest.createImageData(dw, dh);
  for (let y = 0; y < dh; y++) {
    for (let x = 0; x < dw; x++) {
      const gx = x / dw * (sw - 1);
      const gy = y / dh * (sh - 1);
      const x1 = Math.floor(gx);
      const y1 = Math.floor(gy);
      const c = [0, 0, 0, 0];
      for (let m = -1; m <= 2; m++) {
        for (let n = -1; n <= 2; n++) {
          const px = Math.min(Math.max(x1 + m, 0), sw - 1);
          const py = Math.min(Math.max(y1 + n, 0), sh - 1);
          const weight = bicubicKernel(gx - px) * bicubicKernel(gy - py);
          const color = getRGBA(src, px, py);
          for (let i = 0; i < 4; i++) c[i] += color[i] * weight;
        }
      }
      setRGBA(out, x, y, c.map(v => Math.max(0, Math.min(255, v))));
    }
  }
  dest.putImageData(out, 0, 0);
}

function getRGBA(imageData, x, y) {
  const i = (Math.floor(y) * imageData.width + Math.floor(x)) * 4;
  return imageData.data.slice(i, i + 4);
}

function setRGBA(imageData, x, y, rgba) {
  const i = (y * imageData.width + x) * 4;
  rgba.forEach((v, j) => imageData.data[i + j] = v);
}

function bicubicKernel(x) {
  x = Math.abs(x);
  if (x <= 1) return (1.5 * x - 2.5) * x * x + 1;
  if (x < 2) return ((-0.5 * x + 2.5) * x - 4) * x + 2;
  return 0;
}
</script>
