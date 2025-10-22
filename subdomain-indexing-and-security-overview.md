# 子域、測試站防收錄與資安曝光全攻略

## 一、測試站、子域是否會被爬蟲發現？

- 只要網站「公開」，即使沒被外部連結、主站未主動導流，仍有機率被主流爬蟲、資安掃描、第三方資安資料庫自動發現。
- 關鍵在於**DNS公記錄、SSL憑證、GA/GTM第三方追蹤碼、資安流量分析**等技術曝露。

---

## 二、爬蟲與搜尋引擎發現子域與目錄的原理

- 自動掃描主網域下常見子域及目錄（如 dev, test, www, api）
- 讀取**DNS**、**SSL憑證透明度日誌（CT Logs）**、**第三方資安資料庫（SecurityTrails, Shodan, VirusTotal）**、**資安流量分析**、**字典爆破**
- 只要申請過 SSL 憑證，就能被 crt.sh、Google Transparency Log 查詢
- 即使沒主動曝光，仍可被資安工具爆破掃描獲得

---

## 三、DNS、SSL、第三方分析系統如何自動收錄子域

- DNS伺服器的公開紀錄、A/AAAA/MX/CNAME查詢工具暴露所有子域、測試站
- SSL 憑證申請紀錄會被「憑證透明度日誌」完整收錄（如：crt.sh）
- SecurityTrails、Shodan、VirusTotal 等資安服務能即時查詢所有子域紀錄與指紋、第三方資安流量分析可被動記錄尚未曝光分站

---

## 四、GTM、GA等第三方 JS 程式碼會成為被資安工具發現的關聯線索

- 子域只要複製正式站 GATAG/GTM container ID，資安工具可自動比對同 container 使用分站，畫出網路資產關聯
- 公開程式碼能被資安掃描器、主流搜尋引擎爬取

---

## 五、防收錄最安全、最完整建議

### robots.txt 屏蔽

```text
User-agent: *
Disallow: /
```

- 主流搜尋引擎遵守，但不是強制，部分惡意爬蟲會無視

### meta robots 標籤
在所有重要頁面 `<head>` 加入：
```html
<meta name="robots" content="noindex, nofollow">
```
- 禁止索引內容、禁止跟蹤連結；支援正規搜尋引擎

### HTTP 標頭 X-Robots-Tag
針對無法編輯 HTML 的檔案或動態頁面：

```text
X-Robots-Tag: noindex, nofollow
```

### 移除或更換第三方追蹤代碼
- 測試站應避免使用正式站的 GA/GTM/FB Pixel 等追蹤代碼
- 如需分析，建議使用獨立的測試環境專用追蹤 ID
- 移除或註解掉所有可能關聯到正式站的第三方 JS

### 使用非標準連接埠
- 避免使用標準的 80/443 連接埠
- 使用非常見連接埠（如 8080, 3000, 9000）可降低被掃描發現的機率

### 網站內容偽裝
- 在測試站首頁放置「維護中」或「建構中」頁面
- 避免在測試站顯示真實的商業內容或敏感資訊

### 存取控制（密碼或身份驗證)
- Cloudflare Access, Basic Auth, VPN白名單，測試站對外需授權才能存取

### 檢查 robots.txt 與 meta robots 配合
- 若 robots.txt 屏蔽後該頁無法被爬，搜尋引擎就不會看到 meta robots 標籤，noindex標籤多半失效
- 建議不需被索引的頁面兩者同時使用，如部分頁面有特殊需求則精細調整

### 定期資安查詢
- 定期用 Google Search Console, crt.sh, SecurityTrails, DNS查詢分站有無誤收錄
- 檢查 SSL、公DNS紀錄、網站指紋是否意外曝光
- 使用 `site:yourdomain.com` 在 Google 搜尋檢查是否有測試站被收錄
- 檢查 Wayback Machine (archive.org) 是否有快照記錄
- 使用 DNSlytics、RiskIQ 等工具檢查子域曝光情況

### 資安細節（reddit 專家論點）
- DNS記錄若公開即可能被爆破或暴力掃描工具發現
- SSL憑證日誌不可更改且公開，所有分站都無法隱藏
- 只需主網域即可爆破出各種前綴並掃到測試站

---

## 六、實例：crt.sh 查詢 sample.com.tw 主網域所有子域

- 訪問 https://crt.sh/
- 搜尋 sample.com.tw
- 自動列出申請 SSL 的所有分站（例如 dev-pm.sample.com.tw, gitlab.sample.com.tw, ...）
- 結論：凡申請過SSL憑證的子域名一律可被查詢，不論外部有無散布

---

## 七、測試站被收錄後的緊急應對

### 立即處理步驟
1. **加強 robots.txt 和 meta robots 設定**
2. **Google Search Console 申請移除**：使用「移除網址」功能
3. **更改測試站網址**：如情況嚴重，考慮更換子域名
4. **檢查是否有敏感資訊外洩**：客戶資料、內部文件、API 金鑰等

### Google 移除請求流程
- 登入 Google Search Console
- 選擇「移除」→「臨時移除」
- 輸入要移除的網址或目錄
- 選擇移除類型：「從搜尋結果中移除此網址」

---

## 八、總結與最佳防範

### 基礎防護（必做）
- robots.txt 屏蔽大多數主流搜尋引擎
- meta robots 標籤全面設置
- 重要分站HTTP標頭設 X-Robots-Tag

### 進階防護（建議）
- 身份驗證、密碼、白名單等多重安全加持
- 移除或更換第三方追蹤代碼
- 使用非標準連接埠
- 內容偽裝（維護中頁面）

### 持續監控（定期執行）
- 定期資安查詢、SSL憑證和DNS公開紀錄檢查
- 搜尋引擎收錄狀況檢查
- 第三方資安資料庫監控

### 緊急應對（如有需要）
- Google Search Console 移除請求
- 更換測試站網址
- 敏感資訊外洩檢查

安全資產管控應確保所有測試/分站非公開資料都在技術面多層防護，同時留意自動收錄，保護不被主流搜尋收錄與資安工具曝光。建議採用「縱深防禦」策略，結合多種防護方法以達到最佳效果。