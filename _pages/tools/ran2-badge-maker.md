---
title: 亂2 Online 盟徽 製作工具｜16x11 編輯器
layout: splash
permalink: /tools/ran2-badge-maker/
comments: false
share: true

# SEO 相關
excerpt: 為 亂2 Online 製作 16x11 的盟徽（Badge）圖片，支援圖片上傳編輯或空白畫布繪圖，輸出 BMP 格式。
author_profile: false

# SEO meta
title_meta: 亂2 Online 盟徽 製作工具｜16x11 編輯器
canonical_url: https://arlenfuture.github.io/tools/ran2-badge-maker/
---

# 亂2 Online 盟徽 製作工具｜16x11 編輯器

> 上傳圖片進行編輯，或直接在空白畫布上繪圖。輸出固定大小 16x11 BMP 格式。

<style>
body {
    font-family: Arial, sans-serif;
}

.step-container {
    margin: 20px 0;
    padding: 20px;
    border: 2px solid #e0e0e0;
    border-radius: 8px;
    background-color: #f9f9f9;
}

.step-title {
    font-size: 18px;
    font-weight: bold;
    color: #333;
    margin-bottom: 15px;
}

.upload-area {
    border: 2px dashed #ccc;
    border-radius: 8px;
    padding: 30px;
    text-align: center;
    margin: 15px 0;
    transition: border-color 0.3s;
}

.upload-area:hover {
    border-color: #007bff;
}

.upload-area.dragover {
    border-color: #007bff;
    background-color: #f0f8ff;
}

.canvas-container {
    text-align: center;
    margin: 20px 0;
}

#editCanvas {
    border: 2px solid #333;
    cursor: crosshair;
    image-rendering: pixelated;
    background-color: white;
}

.tools {
    display: flex;
    align-items: center;
    gap: 15px;
    margin: 15px 0;
    flex-wrap: wrap;
}

.tool-group {
    display: flex;
    align-items: center;
    gap: 8px;
}

button {
    padding: 8px 16px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 14px;
    margin-right: 8px;
}

.btn-primary {
    background-color: #007bff;
    color: white;
}

.btn-primary:hover {
    background-color: #0056b3;
}

.btn-secondary {
    background-color: #6c757d;
    color: white;
}

.btn-secondary:hover {
    background-color: #545b62;
}

.btn-success {
    background-color: #28a745;
    color: white;
    font-weight: bold;
}

.btn-success:hover {
    background-color: #1e7e34;
}

.eyedropper-active {
    background-color: #ffc107 !important;
    color: #000 !important;
}

#editCanvas.eyedropper-mode {
    cursor: crosshair;
}

input[type="file"] {
    margin: 10px 0;
}

#crop-area {
    position: absolute;
    border: 2px dashed #f00;
    resize: both;
    overflow: hidden;
    cursor: move;
}

#sourceCanvas {
    max-width: 100%;
    border: 1px solid #ccc;
}

.current-step {
    border-color: #007bff;
    background-color: #f0f8ff;
}
</style>

<!-- 步驟 1: 上傳圖片 -->
<div class="step-container current-step" id="step1">
    <div class="step-title">📁 步驟 1: 上傳圖片（可選）</div>
    <div class="upload-area" id="uploadArea">
        <p>拖曳圖片到此處，或點擊下方按鈕選擇檔案</p>
        <input type="file" id="fileInput" accept="image/*">
        <p>不上傳圖片將使用空白畫布</p>
    </div>
    <!-- 圖片預覽和裁切區域 -->
    <div id="cropSection" style="display: none;">
        <div class="tool-group" style="margin: 15px 0;">
            <label for="scaleType">縮放演算法：</label>
            <select id="scaleType">
                <option value="nearest">最近鄰 (Nearest)</option>
                <option value="bilinear">雙線性 (Bilinear)</option>
                <option value="bicubic">模擬雙三次 (Bicubic)</option>
            </select>
        </div>
        <div id="canvas-container" style="position: relative; display: inline-block; margin: 15px 0;">
            <canvas id="sourceCanvas"></canvas>
            <div id="crop-area"></div>
        </div>
        <div style="margin: 15px 0;">
            <strong>預覽：</strong><br>
            <img id="previewImage" width="160" height="110" style="image-rendering: pixelated; border: 1px solid #ccc;">
        </div>
    </div>
    <button class="btn-primary" onclick="startEditing()">🎨 開始編輯</button>
</div>

<!-- 步驟 2: 編輯模式 -->
<div class="step-container" id="step2" style="display: none;">
    <div class="step-title">🎨 步驟 2: 編輯模式</div>
    <div class="tools">
        <div class="tool-group">
            <label>筆刷顏色：</label>
            <input type="color" id="colorPicker" value="#000000">
        </div>
        <div class="tool-group">
            <label>筆刷大小：</label>
            <input type="range" id="brushSize" min="1" max="3" value="1">
            <span id="brushSizeDisplay">1</span>
        </div>
        <div class="tool-group">
            <button class="btn-secondary" id="eyedropperBtn" onclick="toggleEyedropper()">🎨 取色器</button>
        </div>
        <button class="btn-secondary" onclick="clearCanvas()">🧹 清除畫布</button>
        <button class="btn-secondary" onclick="resetCanvas()">🔄 重置</button>
    </div>
    <div class="canvas-container">
        <canvas id="editCanvas" width="16" height="11" style="width: 320px; height: 220px;"></canvas>
    </div>
    <p><strong>說明：</strong>直接在畫布上點擊或拖曳來繪圖。畫布尺寸為 16x11 像素。</p>
</div>

<!-- 步驟 3: 下載 -->
<div class="step-container" id="step3" style="display: none;">
    <div class="step-title">📥 步驟 3: 下載檔案</div>
    <p>點擊下方按鈕下載您的 16x11 BMP 盟徽檔案：</p>
    <!-- 下載位置提醒 -->
    <div class="bg-yellow-100 text-yellow-800 p-4 rounded-xl shadow mt-4">
        <ul class="list-disc list-inside mt-2">
            <li>將輸出的 BMP 檔案儲存到以下位置：</li>
            <li class="ml-4">C:\Users\使用者名稱\Documents</li>
            <li class="ml-4">或者直接在 Windows 11 中點擊「文件」資料夾</li>
        </ul>
    </div>
    <button class="btn-success" onclick="downloadBMP()">📥 下載 BMP 檔案</button>
</div>

<script>
let editCanvas, editCtx;
let isDrawing = false;
let originalImageData = null;
let sourceCanvas, sourceCtx, cropArea, previewImage, scaleType;
let isDragging = false;
let dragOffsetX, dragOffsetY;
let isEyedropperMode = false;

// 初始化
document.addEventListener('DOMContentLoaded', function() {
    editCanvas = document.getElementById('editCanvas');
    editCtx = editCanvas.getContext('2d');
    editCtx.imageSmoothingEnabled = false;
    
    // 初始化裁切相關元素
    sourceCanvas = document.getElementById('sourceCanvas');
    sourceCtx = sourceCanvas.getContext('2d');
    cropArea = document.getElementById('crop-area');
    previewImage = document.getElementById('previewImage');
    scaleType = document.getElementById('scaleType');
    
    // 初始化空白畫布
    editCtx.fillStyle = '#FFFFFF';
    editCtx.fillRect(0, 0, 16, 11);
    
    // 設置拖拽上傳
    setupDragAndDrop();
    
    // 設置畫布事件
    setupCanvasEvents();
    
    // 設置裁切功能
    setupCropEvents();
    
    // 設置筆刷大小顯示更新
    document.getElementById('brushSize').addEventListener('input', function() {
        document.getElementById('brushSizeDisplay').textContent = this.value;
    });
});

// 設置拖拽上傳
function setupDragAndDrop() {
    const uploadArea = document.getElementById('uploadArea');
    const fileInput = document.getElementById('fileInput');
    
    uploadArea.addEventListener('dragover', function(e) {
        e.preventDefault();
        uploadArea.classList.add('dragover');
    });
    
    uploadArea.addEventListener('dragleave', function(e) {
        e.preventDefault();
        uploadArea.classList.remove('dragover');
    });
    
    uploadArea.addEventListener('drop', function(e) {
        e.preventDefault();
        uploadArea.classList.remove('dragover');
        const files = e.dataTransfer.files;
        if (files.length > 0) {
            handleImageFile(files[0]);
        }
    });
    
    fileInput.addEventListener('change', function() {
        if (this.files.length > 0) {
            handleImageFile(this.files[0]);
        }
    });
}

// 處理圖片檔案
function handleImageFile(file) {
    if (!file.type.startsWith('image/')) {
        alert('請選擇圖片檔案');
        return;
    }
    
    const reader = new FileReader();
    reader.onload = function(e) {
        const img = new Image();
        img.onload = function() {
            // 顯示裁切區域
            document.getElementById('cropSection').style.display = 'block';
            
            // 設置來源畫布
            sourceCanvas.width = img.width;
            sourceCanvas.height = img.height;
            sourceCtx.drawImage(img, 0, 0);
            
            // 初始化裁切框
            const initialSize = Math.min(img.width, img.height * 16 / 11);
            cropArea.style.width = Math.min(160, initialSize) + 'px';
            cropArea.style.height = Math.min(110, initialSize * 11 / 16) + 'px';
            cropArea.style.left = '10px';
            cropArea.style.top = '10px';
            
            updatePreview();
        };
        img.src = e.target.result;
    };
    reader.readAsDataURL(file);
}

// 開始編輯
function startEditing() {
    // 如果有預覽圖片，使用預覽的結果
    if (previewImage.src && previewImage.src !== window.location.href) {
        const tempImg = new Image();
        tempImg.onload = function() {
            editCtx.clearRect(0, 0, 16, 11);
            editCtx.drawImage(tempImg, 0, 0, 16, 11);
            originalImageData = editCtx.getImageData(0, 0, 16, 11);
        };
        tempImg.src = previewImage.src;
    }
    
    document.getElementById('step1').style.display = 'none';
    document.getElementById('step2').style.display = 'block';
    document.getElementById('step3').style.display = 'block';
    
    document.getElementById('step1').classList.remove('current-step');
    document.getElementById('step2').classList.add('current-step');
    
    // 如果沒有圖片數據，保存當前空白畫布狀態
    if (!originalImageData) {
        originalImageData = editCtx.getImageData(0, 0, 16, 11);
    }
}

// 設置畫布繪圖事件
function setupCanvasEvents() {
    // 滑鼠事件
    editCanvas.addEventListener('mousedown', function(e) {
    if (isEyedropperMode) {
        pickColor(e);
        } else {
            startDrawing(e);
        }
    });
    editCanvas.addEventListener('mousemove', draw);
    editCanvas.addEventListener('mouseup', stopDrawing);
    editCanvas.addEventListener('mouseout', stopDrawing);
    
    // 觸控事件（手機支援）
    editCanvas.addEventListener('touchstart', function(e) {
        e.preventDefault();
        const touch = e.touches[0];
        const mouseEvent = new MouseEvent('mousedown', {
            clientX: touch.clientX,
            clientY: touch.clientY
        });
        editCanvas.dispatchEvent(mouseEvent);
    });
    
    editCanvas.addEventListener('touchmove', function(e) {
        e.preventDefault();
        const touch = e.touches[0];
        const mouseEvent = new MouseEvent('mousemove', {
            clientX: touch.clientX,
            clientY: touch.clientY
        });
        editCanvas.dispatchEvent(mouseEvent);
    });
    
    editCanvas.addEventListener('touchend', function(e) {
        e.preventDefault();
        const mouseEvent = new MouseEvent('mouseup', {});
        editCanvas.dispatchEvent(mouseEvent);
    });
}

function startDrawing(e) {
    isDrawing = true;
    draw(e);
}

function draw(e) {
    if (!isDrawing) return;
    
    const rect = editCanvas.getBoundingClientRect();
    const scaleX = editCanvas.width / rect.width;
    const scaleY = editCanvas.height / rect.height;
    
    const x = Math.floor((e.clientX - rect.left) * scaleX);
    const y = Math.floor((e.clientY - rect.top) * scaleY);
    
    const brushSize = parseInt(document.getElementById('brushSize').value);
    const color = document.getElementById('colorPicker').value;
    
    editCtx.fillStyle = color;
    editCtx.fillRect(x, y, brushSize, brushSize);
}

function stopDrawing() {
    isDrawing = false;
}

// 清除畫布
function clearCanvas() {
    editCtx.fillStyle = '#FFFFFF';
    editCtx.fillRect(0, 0, 16, 11);
}

// 重置畫布
function resetCanvas() {
    if (originalImageData) {
        editCtx.putImageData(originalImageData, 0, 0);
    } else {
        clearCanvas();
    }
}

// 下載 24-bit BMP（跨瀏覽器固定）
function downloadBMP() {
    const canvas = editCanvas;
    const width = canvas.width;
    const height = canvas.height;
    const ctx = canvas.getContext("2d");
    const imageData = ctx.getImageData(0, 0, width, height);
    const pixels = imageData.data;

    // 每行必須是 4 bytes 對齊 (BMP 規定)
    const rowSize = Math.floor((24 * width + 31) / 32) * 4;
    const pixelArraySize = rowSize * height;
    const fileSize = 54 + pixelArraySize;

    const buffer = new ArrayBuffer(fileSize);
    const dv = new DataView(buffer);

    let p = 0;
    // BMP Header
    dv.setUint8(p++, 0x42); // 'B'
    dv.setUint8(p++, 0x4D); // 'M'
    dv.setUint32(p, fileSize, true); p += 4;
    dv.setUint16(p, 0, true); p += 2; // reserved1
    dv.setUint16(p, 0, true); p += 2; // reserved2
    dv.setUint32(p, 54, true); p += 4; // offset to pixel data

    // DIB Header (BITMAPINFOHEADER)
    dv.setUint32(p, 40, true); p += 4; // header size
    dv.setInt32(p, width, true); p += 4;
    dv.setInt32(p, -height, true); p += 4; // 負數 = top-down bitmap
    dv.setUint16(p, 1, true); p += 2; // planes
    dv.setUint16(p, 24, true); p += 2; // bits per pixel
    dv.setUint32(p, 0, true); p += 4; // compression (none)
    dv.setUint32(p, pixelArraySize, true); p += 4;
    dv.setInt32(p, 2835, true); p += 4; // X ppm (72 DPI)
    dv.setInt32(p, 2835, true); p += 4; // Y ppm
    dv.setUint32(p, 0, true); p += 4; // colors in palette
    dv.setUint32(p, 0, true); p += 4; // important colors

    // Pixel Data (BGR, no alpha, padded)
    let offset = 54;
    const padding = rowSize - width * 3;

    for (let y = 0; y < height; y++) {
        for (let x = 0; x < width; x++) {
            const i = (y * width + x) * 4;
            dv.setUint8(offset++, pixels[i + 2]); // B
            dv.setUint8(offset++, pixels[i + 1]); // G
            dv.setUint8(offset++, pixels[i]);     // R
        }
        offset += padding;
    }

    // 建立下載
    const blob = new Blob([buffer], { type: "image/bmp" });
    const link = document.createElement("a");
    link.href = URL.createObjectURL(blob);
    link.download = "ran2_badge_16x11.bmp";
    link.click();
}

// 設置裁切功能事件
function setupCropEvents() {
    // 拖曳裁切框
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
        const rect = sourceCanvas.getBoundingClientRect();
        
        let newLeft = e.clientX - rect.left - dragOffsetX;
        let newTop = e.clientY - rect.top - dragOffsetY;
        
        newLeft = Math.max(0, Math.min(newLeft, sourceCanvas.width - cropArea.offsetWidth));
        newTop = Math.max(0, Math.min(newTop, sourceCanvas.height - cropArea.offsetHeight));
        
        cropArea.style.left = `${newLeft}px`;
        cropArea.style.top = `${newTop}px`;
    });
    
    // 調整大小，維持比例
    new ResizeObserver(() => {
        const width = cropArea.offsetWidth;
        const newHeight = Math.round(width * 11 / 16);
        cropArea.style.height = `${newHeight}px`;
        
        // 限制不要超出畫布
        const left = cropArea.offsetLeft;
        const top = cropArea.offsetTop;
        const maxWidth = sourceCanvas.width - left;
        const maxHeight = sourceCanvas.height - top;
        
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
    
    // 縮放演算法改變時更新預覽
    scaleType.addEventListener('change', updatePreview);
}

// 更新預覽
function updatePreview() {
    if (!sourceCanvas.width) return;
    
    const rect = cropArea.getBoundingClientRect();
    const canvasRect = sourceCanvas.getBoundingClientRect();
    const scaleX = sourceCanvas.width / canvasRect.width;
    const scaleY = sourceCanvas.height / canvasRect.height;
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
        outCtx.drawImage(sourceCanvas, sx, sy, sw, sh, 0, 0, 16, 11);
    } else if (scaleType.value === "bilinear") {
        drawBilinear(sourceCanvas, sx, sy, sw, sh, output, 16, 11);
    } else {
        drawBicubic(sourceCanvas, sx, sy, sw, sh, output, 16, 11);
    }
    
    previewImage.src = output.toDataURL();
}

// 雙線性插值算法
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

// 雙三次插值算法
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

// 切換取色器模式
function toggleEyedropper() {
    isEyedropperMode = !isEyedropperMode;
    const btn = document.getElementById('eyedropperBtn');
    
    if (isEyedropperMode) {
        btn.classList.add('eyedropper-active');
        btn.textContent = '🎨 取色中...';
        editCanvas.classList.add('eyedropper-mode');
    } else {
        btn.classList.remove('eyedropper-active');
        btn.textContent = '🎨 取色器';
        editCanvas.classList.remove('eyedropper-mode');
    }
}

// 取色功能
function pickColor(e) {
    const rect = editCanvas.getBoundingClientRect();
    const scaleX = editCanvas.width / rect.width;
    const scaleY = editCanvas.height / rect.height;
    
    const x = Math.floor((e.clientX - rect.left) * scaleX);
    const y = Math.floor((e.clientY - rect.top) * scaleY);
    
    // 獲取該像素的顏色
    const imageData = editCtx.getImageData(x, y, 1, 1);
    const [r, g, b] = imageData.data;
    
    // 轉換為十六進制顏色
    const hexColor = `#${((1 << 24) + (r << 16) + (g << 8) + b).toString(16).slice(1)}`;
    
    // 設置顏色選擇器的值
    document.getElementById('colorPicker').value = hexColor;
    
    // 自動退出取色器模式
    toggleEyedropper();
}
</script>