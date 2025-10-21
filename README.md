# 電商網站 SEO 優化標準模板

> 適用於購物網站的商品頁面和商品列表頁面的 SEO 最佳化實作範例

## 📋 目錄

- [專案概述](#專案概述)
- [檔案結構](#檔案結構)
- [SEO 優化要素](#seo-優化要素)
- [實作指南](#實作指南)
- [維護建議](#維護建議)
- [效能監控](#效能監控)

## 🎯 專案概述

本專案提供電商網站（以黃金白銀交易平台為例）的 SEO 標準化模板，包含：

- **商品列表頁**（`head-seo-category.html`）：類別頁面的完整 SEO 配置
- **商品詳情頁**（`head-seo-product.html`）：單一商品頁面的完整 SEO 配置

### ✨ 主要特色

- ✅ 完整的基礎 Meta 標籤配置
- ✅ Open Graph 社群分享優化
- ✅ 結構化資料（Schema.org）標記
- ✅ 效能優化配置（Preconnect、Preload）
- ✅ AI 搜尋引擎友好設定
- ✅ 符合 E-E-A-T 指導原則

## 📁 檔案結構

```
📦 SEO優化模板
├── 📄 head-seo-category.html    # 商品列表頁 SEO 模板
├── 📄 head-seo-product.html     # 商品詳情頁 SEO 模板
├── 📄 README.md                 # 本說明文件
└── 📄 SEO-CHECKLIST.md         # SEO 檢查清單（建議新增）
```

## 🔧 SEO 優化要素

### 1. 基礎 Meta 標籤 🏗️

#### 商品列表頁範例
```html
<title>黃金買賣與金條商品清單 | NotARealName黃金白銀交易所</title>
<meta name="description" content="沒有這一間黃金買賣專區，提供多樣化高品質金條、金幣與黃金禮品。台灣現貨，透明報價，支援門市取貨。">
<meta name="robots" content="index, follow, max-snippet:200, max-image-preview:large">
```

#### 商品詳情頁範例
```html
<title>2025馬馬馬馬金鷹銀幣1盎司 - 純銀收藏幣 | NotARealName黃金白銀交易所</title>
<meta name="description" content="2025馬馬馬馬金鷹銀幣：波蘭日耳曼尼亞鑄幣廠發行稀有1盎司純銀收藏幣，主題為金鷹與毒蛇搏鬥。台灣現貨，收藏投資皆宜。">
```

**🎯 優化要點：**
- Title 控制在 50-60 字元內
- Description 建議 120-160 字元
- 包含主要關鍵字和品牌名稱
- 加入地域性關鍵字（如：台灣現貨）

### 2. Open Graph 社群分享優化 📱

```html
<meta property="og:site_name" content="NotARealName黃金白銀交易所">
<meta property="og:title" content="商品名稱 - 品牌名稱">
<meta property="og:type" content="product"> <!-- 商品頁用 product，列表頁用 website -->
<meta property="og:image" content="商品主圖URL">
<meta property="og:description" content="吸引人的商品描述">
```

**🎯 優化要點：**
- 圖片建議 1200x630 像素
- 只使用一張主要圖片避免混亂
- 描述要簡潔有力，突出賣點

### 3. 結構化資料標記 🏷️

#### 商品頁結構化資料
```json
{
  "@context": "https://schema.org/",
  "@type": "Product",
  "name": "商品名稱",
  "description": "商品描述",
  "sku": "商品編號",
  "offers": {
    "@type": "Offer",
    "price": "價格",
    "priceCurrency": "TWD",
    "availability": "庫存狀態"
  }
}
```

#### 支援的 Schema 類型
- ✅ **Product**：商品基本資訊
- ✅ **CollectionPage**：商品列表頁
- ✅ **BreadcrumbList**：麵包屑導覽
- ✅ **FAQPage**：常見問題
- ✅ **Organization**：公司資訊

### 4. 效能優化配置 ⚡

```html
<!-- 預連接重要域名 -->
<link rel="preconnect" href="https://sub.NotARealName.com.tw" />
<link rel="preconnect" href="https://www.NotARealName.com.tw" />

<!-- 預載入關鍵資源 -->
<link rel="preload" href="主要商品圖片URL" as="image">

<!-- 預取相關頁面 -->
<link rel="prefetch" href="相關類別頁面URL">
```

### 5. AI 搜尋優化 🤖

```html
<meta name="robots" content="index, follow, max-snippet:200, max-image-preview:large">
<meta name="referrer" content="no-referrer-when-downgrade">
```

**🎯 AI 友好特性：**
- 允許大圖預覽提升視覺效果
- 豐富的結構化資料幫助 AI 理解內容
- FAQ 結構化資料支援 AI 直接回答

## 📚 實作指南

### Step 1: 選擇適合的模板
- **商品列表頁** → 使用 `head-seo-category.html`
- **商品詳情頁** → 使用 `head-seo-product.html`

### Step 2: 自訂化配置

#### 必須修改的項目 ⚠️
1. **網域名稱**：將 `NotARealName.com.tw` 改為實際域名
2. **品牌名稱**：更新為實際公司/品牌名稱
3. **商品資訊**：更新商品名稱、描述、價格等
4. **圖片 URL**：更新為實際的商品圖片連結
5. **聯絡資訊**：更新公司地址、電話等資訊

#### 建議自訂的項目 📝
1. **關鍵字策略**：根據目標關鍵字調整 title 和 description
2. **地域性優化**：加入目標市場的地理關鍵字
3. **品牌 Schema**：補充完整的公司 Logo 和聯絡方式
4. **FAQ 內容**：根據實際客戶常見問題擴充

### Step 3: 動態資料整合

**建議後端動態生成的欄位：**
```php
// 範例：PHP 動態生成
<title><?= $product['name'] ?> | <?= $site['brand_name'] ?></title>
<meta name="description" content="<?= $product['seo_description'] ?>">
<meta property="og:image" content="<?= $product['main_image'] ?>">

<script type="application/ld+json">
{
  "@type": "Product",
  "name": "<?= $product['name'] ?>",
  "price": "<?= $product['current_price'] ?>",
  "availability": "<?= $product['stock_status'] ?>"
}
</script>
```

## 🔄 維護建議

### 定期檢查項目 📅

#### 每週檢查
- [ ] 商品價格和庫存狀態更新
- [ ] 新商品的 SEO 標籤設定
- [ ] 404 錯誤頁面檢查

#### 每月檢查
- [ ] 搜尋引擎索引狀況
- [ ] 結構化資料測試
- [ ] 網站速度測試
- [ ] 競爭對手 SEO 分析

#### 每季檢查
- [ ] 關鍵字排名監控
- [ ] SEO 效果數據分析
- [ ] Schema 標記更新
- [ ] 內容策略調整

### 常見問題排查 🔍

**1. 結構化資料錯誤**
- 使用 [Google Rich Results Test](https://search.google.com/test/rich-results) 檢測
- 確保所有必填欄位都有有效值
- 避免使用佔位文字（如："請輸入價格"）

**2. 重複內容問題**
- 正確設定 canonical 標籤
- 避免多個 URL 指向相同內容
- 合理使用 robots.txt 控制爬取

**3. 圖片優化**
- 使用適當的圖片尺寸和格式
- 添加 alt 屬性提升可訪問性
- 實施圖片懶載入提升效能

## 📊 效能監控

### 推薦工具

#### SEO 分析工具 🔧
- **Google Search Console**：監控搜尋表現
- **Google Analytics**：流量分析
- **PageSpeed Insights**：網站速度評估
- **SEMrush / Ahrefs**：關鍵字排名監控

#### 結構化資料測試 ✅
- **Google Rich Results Test**：測試結構化資料
- **Schema.org Validator**：驗證 Schema 標記
- **Facebook Sharing Debugger**：測試 OG 標籤

### 關鍵指標 (KPI)

#### SEO 成效指標 📈
- 🎯 **有機搜尋流量成長率**
- 🎯 **目標關鍵字排名提升**
- 🎯 **商品頁面點擊率 (CTR)**
- 🎯 **搜尋結果豐富摘要顯示率**

#### 轉換指標 💰
- 🛍️ **SEO 流量轉換率**
- 🛍️ **平均訂單價值 (AOV)**
- 🛍️ **購物車放棄率**

## 📝 更新日誌

### 2024.10.21
- ✨ 初版發布
- ✅ 完成商品頁和列表頁模板
- ✅ 加入 AI 搜尋優化配置
- ✅ 完整的結構化資料支援

---

## 🤝 貢獻指南

歡迎提交 Issue 和 Pull Request 來改進這個 SEO 模板！

### 貢獻方式
1. Fork 本專案
2. 創建功能分支 (`git checkout -b feature/amazing-seo-feature`)
3. 提交變更 (`git commit -m 'Add some amazing SEO feature'`)
4. 推送到分支 (`git push origin feature/amazing-seo-feature`)
5. 開啟 Pull Request

## 📄 授權

本專案採用 MIT 授權條款 - 詳見 [LICENSE](LICENSE) 檔案

---

**⭐ 如果這個 SEO 模板對您有幫助，請給個星星支持！**