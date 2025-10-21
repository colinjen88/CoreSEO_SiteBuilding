# 語意化HTML結構指南 - 簡化版

> 專注於核心語意結構，展現電商網站的標準HTML架構

## 🏗️ 整體結構概覽

```html
<!DOCTYPE html>
<html lang="zh-TW">
<head>...</head>
<body>
    <header>     <!-- 網站標頭 -->
    <aside>      <!-- 側邊欄篩選 -->
    <main>       <!-- 主要內容 -->
    <footer>     <!-- 網站頁尾 -->
</body>
</html>
```

## 📋 核心結構說明

### 1. Header（網站標頭）
```html
<header>
    <div>
        <!-- Logo -->
        <div>
            <a href="/" aria-label="首頁">
                <img src="/logo.png" alt="NotThing黃金白銀交易所">
            </a>
        </div>
        
        <!-- 主要導覽 -->
        <nav aria-label="主要導覽">
            <ul>
                <li><a href="/gold">黃金商品</a></li>
                <li><a href="/silver">白銀商品</a></li>
            </ul>
        </nav>
        
        <!-- 搜尋功能 -->
        <div>
            <form role="search">
                <input type="search" aria-label="搜尋商品">
                <button type="submit" aria-label="執行搜尋">搜尋</button>
            </form>
        </div>
        
        <!-- 會員功能 -->
        <nav aria-label="會員功能">
            <ul>
                <li><a href="/login">登入</a></li>
                <li><a href="/cart">購物車</a></li>
            </ul>
        </nav>
    </div>
    
    <!-- 即時價格 -->
    <section aria-label="即時價格">
        <h2>貴金屬即時價格</h2>
    </section>
</header>
```

### 2. Aside（側邊欄）
```html
<aside aria-label="商品篩選">
    <!-- 篩選表單 -->
    <section>
        <h2>篩選商品</h2>
        <form>
            <fieldset>
                <legend>價格範圍</legend>
                <label for="price-min">最低價格</label>
                <input type="number" id="price-min">
            </fieldset>
            <fieldset>
                <legend>商品類型</legend>
                <label><input type="checkbox" value="gold"> 黃金</label>
                <label><input type="checkbox" value="silver"> 白銀</label>
            </fieldset>
            <button type="submit">套用篩選</button>
        </form>
    </section>

    <!-- 分類導覽 -->
    <nav aria-label="商品分類">
        <h2>商品分類</h2>
        <ul>
            <li><a href="/category/gold-bars">金條</a></li>
            <li><a href="/category/gold-coins">金幣</a></li>
        </ul>
    </nav>
</aside>
```

### 3. Main（主要內容）
```html
<main>
    <!-- 頁面主標題 -->
    <h1 class="visually-hidden">商品目錄</h1>
    
    <!-- 麵包屑導覽 -->
    <nav aria-label="breadcrumb">
        <ol>
            <li><a href="/">首頁</a></li>
            <li><a href="/category">分類</a></li>
            <li aria-current="page">目前頁面</li>
        </ol>
    </nav>
    
    <!-- 商品列表區域 -->
    <section aria-label="商品列表">
        <h2 class="visually-hidden">商品列表</h2>

        <!-- 排序選項 -->
        <div>
            <label for="sort-select">排序方式：</label>
            <select id="sort-select">
                <option value="price-asc">價格：低到高</option>
                <option value="newest">最新上架</option>
            </select>
        </div>

        <!-- 商品清單 -->
        <ul>
            <li>
                <article itemscope itemtype="https://schema.org/Product">
                    <img src="/product.jpg" alt="商品名稱" itemprop="image">
                    
                    <h3 itemprop="name">
                        <a href="/product/link">商品名稱</a>
                    </h3>

                    <!-- 價格資訊 -->
                    <div itemprop="offers" itemscope itemtype="https://schema.org/Offer">
                        <span itemprop="price" content="85000">NT$ 85,000</span>
                        <meta itemprop="priceCurrency" content="TWD">
                        <meta itemprop="availability" content="https://schema.org/InStock">
                    </div>

                    <!-- 評價資訊 -->
                    <div itemprop="aggregateRating" itemscope itemtype="https://schema.org/AggregateRating">
                        <span aria-label="評分 4.8 分">★★★★★</span>
                        <span>(<span itemprop="ratingValue">4.8</span>) <span itemprop="reviewCount">128</span>則評價</span>
                    </div>

                    <!-- 商品描述 -->
                    <p itemprop="description">商品簡短描述</p>

                    <!-- 操作按鈕 -->
                    <div>
                        <button type="button" aria-label="加入購物車">加入購物車</button>
                        <button type="button" aria-label="加入收藏">收藏</button>
                    </div>
                </article>
            </li>
        </ul>
    </section>
    
    <!-- 分頁導覽 -->
    <nav aria-label="分頁導覽">
        <ul>
            <li><a href="?page=2" aria-label="上一頁">← 上一頁</a></li>
            <li><a href="?page=1" aria-label="第 1 頁">1</a></li>
            <li><span aria-current="page" aria-label="目前頁面">3</span></li>
            <li><a href="?page=4" aria-label="下一頁">下一頁 →</a></li>
        </ul>
        <div aria-live="polite">顯示第 21-30 項，共 150 項商品</div>
    </nav>
</main>
```

### 4. Footer（網站頁尾）
```html
<footer>
    <!-- 公司資訊 -->
    <section aria-label="公司資訊">
        <a href="/">
            <img src="/logo.png" alt="NotThing黃金白銀交易所">
        </a>
        
        <div>
            <h2 class="visually-hidden">特色理念</h2>
            <ul>
                <li><a href="/feature1"><img alt="同步國際商品"></a></li>
                <li><a href="/feature2"><img alt="即時價格公開"></a></li>
            </ul>
        </div>
    </section>

    <!-- 社群連結 -->
    <nav aria-label="社群媒體">
        <ul>
            <li><a href="https://facebook.com/example" aria-label="Facebook">FB</a></li>
            <li><a href="https://instagram.com/example" aria-label="Instagram">IG</a></li>
        </ul>
    </nav>

    <!-- 聯絡資訊 -->
    <section aria-label="聯絡我們">
        <h2>聯絡我們</h2>
        <address>
            服務電話：<a href="tel:+88661234567">06-123-4567</a><br>
            客服信箱：<a href="mailto:service@example.com">service@example.com</a>
        </address>
    </section>

    <!-- 門市資訊 -->
    <section aria-label="門市資訊">
        <h2>實體門市</h2>
        <div>
            <h3>台北門市</h3>
            <address>
                電話：<a href="tel:+886200000000">(02) 0000-0000</a><br>
                地址：台北市中正區一二三街123號
            </address>
        </div>
    </section>
</footer>
```

## 🔑 重要語意元素說明

### aria-label 使用原則
- **導覽區域**：`aria-label="主要導覽"`, `aria-label="商品分類"`
- **功能區域**：`aria-label="商品篩選"`, `aria-label="會員功能"`
- **資訊區域**：`aria-label="公司資訊"`, `aria-label="聯絡我們"`
- **按鈕操作**：`aria-label="加入購物車"`, `aria-label="執行搜尋"`
- **頁面狀態**：`aria-current="page"`, `aria-live="polite"`

### 表單語意化
```html
<fieldset>
    <legend>欄位群組標題</legend>
    <label for="input-id">標籤文字</label>
    <input type="text" id="input-id" name="input-name">
</fieldset>
```

### 結構化資料
```html
<!-- 商品結構化資料 -->
<article itemscope itemtype="https://schema.org/Product">
    <h3 itemprop="name">商品名稱</h3>
    <img itemprop="image" src="product.jpg" alt="商品描述">
    <div itemprop="offers" itemscope itemtype="https://schema.org/Offer">
        <span itemprop="price" content="價格數字">顯示價格</span>
        <meta itemprop="priceCurrency" content="TWD">
        <meta itemprop="availability" content="https://schema.org/InStock">
    </div>
</article>
```

## ✅ SEO 優化重點

### 1. 標題階層
- H1：頁面主標題（可隱藏但保留語意）
- H2：主要區塊標題
- H3：商品名稱或子區塊標題

### 2. 內部連結
- Logo 連回首頁
- 麵包屑導覽提供層級路徑
- 商品標題連到詳細頁面
- 分類導覽建立網站結構

### 3. 圖片優化
- 所有圖片都有適當的 alt 屬性
- 商品圖片包含結構化資料標記
- Logo 圖片包含品牌名稱

### 4. 無障礙性
- 適當的 aria-label 標籤
- 表單元素正確關聯
- 鍵盤導覽友善
- 螢幕閱讀器支援

## 💡 使用建議

### 適用場景
- 電商商品列表頁
- 分類瀏覽頁面
- 搜尋結果頁面

### 客製化要點
1. 依據實際業務調整導覽項目
2. 根據商品特性調整篩選條件
3. 配合品牌風格調整內容文字
4. 結構化資料根據實際商品資訊填寫

### 維護要點
- 保持 aria-label 的簡潔明確
- 確保表單 label 和 input 的正確關聯
- 結構化資料與實際內容保持同步
- 定期檢查內部連結的有效性

這個簡化版本專注於展現核心的語意化結構，避免過度複雜的設計，更容易理解和應用到實際專案中。