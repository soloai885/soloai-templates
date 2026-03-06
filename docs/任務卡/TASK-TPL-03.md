# 任務卡：TASK-TPL-03 版型B（美甲）完整建置

## 來源
- 任務指令：TASK-TEMPLATE-BUILD-三套版型自建.md
- 對應 PHASE/STEP：Phase 3

## 前置條件
- ✅ TASK-TPL-01（Phase 1）已驗收通過
- ✅ TASK-TPL-02（Phase 2 版型A）已驗收通過
- ✅ template-b-nail 基礎架構已就緒

## 目標
將版型B（美甲）從骨架建置為完整可瀏覽的深色主題商家官網，包含 Masonry 作品集 + 標籤篩選特色模組。

## ⚠️ 小C 技術重點提醒（必須遵守）
1. **深色主題**（`#1A1A2E` 黑冷灰背景），直接設 bg 色，不用 Tailwind `dark:` 模式
2. **Masonry 用 CSS `columns` 實作**，不用 JS library（如 Masonry.js），避免 SSR 問題
3. **標籤篩選用原生 JS**（`classList.toggle`），不引入外部套件

## 執行步驟

### STEP 1：建立 Navbar 元件
檔案：`src/components/Navbar.astro`
- 深色背景（`#1A1A2E`）
- Logo 居中
- 電話 CTA + LINE 按鈕
- Mobile 漢堡選單
- 導航連結：服務項目(#services) / 作品集(#gallery) / 位置資訊(#location)

### STEP 2：建立 Hero 元件
檔案：`src/components/Hero.astro`
- 黑底大圖背景
- 霓虹紫（`#D98EF0`）裝飾線條/accent
- 店名 + tagline + 預約按鈕
- 深色 overlay

### STEP 3：建立熱門服務卡元件
檔案：`src/components/Services.astro`
- `id="services"`
- 暗色卡片（深色背景 + 淺色文字）
- 從 site.ts services 讀取
- hover 效果：霓虹紫邊框或光暈

### STEP 4：建立 Masonry 作品集 + 標籤篩選元件（特色模組）
檔案：`src/components/Gallery.astro`
- `id="gallery"`
- 標籤篩選列：[全部] [法式] [漸層] [節日款] [簡約]
  - 使用原生 JS `classList.toggle` 實作篩選
  - 點擊標籤 → 顯示/隱藏對應 data-tag 的圖片
  - 「全部」顯示所有
- Masonry 排列：
  - 使用 CSS `columns`（不用 JS library）
  - Desktop：3 欄
  - Tablet：2 欄
  - Mobile：1 欄
- 圖片使用 placeholder，每張標記不同 tag

### STEP 5：建立信任模組元件
檔案：`src/components/TrustSection.astro`
- 深色背景
- 信任點（從 site.ts 讀取）
- 客戶評價引言

### STEP 6：建立位置資訊元件
檔案：`src/components/Location.astro`
- `id="location"`
- 深色背景區塊
- 地址 + 營業時間 + Google Map iframe
- 電話直撥 + LINE CTA 按鈕（霓虹紫 accent 色）

### STEP 7：建立 Footer 元件
檔案：`src/components/Footer.astro`
- 最深色背景
- LINE + 電話 + 版權

### STEP 8：整合至首頁
更新 `src/pages/index.astro`：
1. Navbar
2. Hero
3. Services（熱門服務卡）
4. Gallery（Masonry 作品集 + 標籤篩選）
5. TrustSection
6. Location
7. Footer

### STEP 9：測試
- `npm run build` 無 error
- Desktop / Mobile RWD 確認
- Masonry 排列正確
- 標籤篩選功能正常

## 驗收標準
- [ ] 7 個 Section 元件全部建立
- [ ] 深色主題一致（黑冷灰 `#1A1A2E` 為主背景）
- [ ] 所有資料從 site.ts 讀取
- [ ] Masonry 作品集使用 CSS `columns`（非 JS library）
- [ ] 標籤篩選用原生 JS 實作，可正常切換顯示/隱藏
- [ ] 「全部」標籤顯示所有作品
- [ ] 霓虹紫（`#D98EF0`）用於 hover/accent 效果
- [ ] 電話直撥（tel:）+ LINE 按鈕存在
- [ ] Mobile（375px）無橫向溢出
- [ ] 佔位圖正確顯示
- [ ] `npm run build` 無 error
- [ ] 深色背景上文字清晰可讀

## 注意事項
1. **不動 Phase 1 架構檔案**（site.ts 結構、tailwind.config、BaseLayout 的 CSS variables）
2. **純 Tailwind utility**，不引入 UI component library
3. **Masonry 不用 Masonry.js**，用 CSS columns 避免 SSR 問題
4. **標籤篩選不引入外部套件**，用原生 JS classList
5. **深色主題注意對比度**，確保文字在深色背景上可讀

---

*任務卡由小K產出，派給小碼執行。*
*完成後由小K驗收（含瀏覽器視覺測試 + Masonry + 標籤篩選功能測試），驗收通過後再拆 TASK-TPL-04（Phase 4：版型C）。*
