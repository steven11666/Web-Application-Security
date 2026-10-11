# OWASP Juice Shop — SQL Injection Analysis Lab

## 1. Project Overview

本專案以本機 OWASP Juice Shop 為練習環境，研究登入功能中的 SQL Injection 風險，透過瀏覽器開發者工具觀察 HTTP 請求與回應，並閱讀login route原始碼，分析可能的漏洞成因及防禦方式。


## 2. Objectives

* 理解 HTTP 登入請求與回應。
* 使用 Chrome DevTools 觀察登入行為。
* 閱讀 JavaScript 後端程式碼及 SQL 查詢。
* 分析字串插值可能造成的 SQL Injection 風險。
* 理解參數化查詢的防禦原理。
* 建立可重現、可驗證的資安實驗紀錄。

## 3. Environment

* Application: OWASP Juice Shop
* Deployment: Docker
* Browser: Google Chrome
* Analysis Tool: Chrome DevTools
* Language: JavaScript / SQL


## 4. Methodology

### Step 1: 透過 Chrome DevTools 的 Network 面板觀察登入請求，確認登入端點、HTTP 狀態碼與回應內容。

### Step 2: 比較一般無效信箱與包含單引號的測試輸入所產生的回應差異。

### Step 3: Analyze Source Code，閱讀login route，檢查使用者輸入如何進入 SQL 查詢字串，並確認查詢是否採用參數化處理。

### Step 4: 結合實驗結果與原始碼，分析輸入內容影響 SQL 查詢解析的可能性，區分已觀察到的事實與尚待驗證的推論。

### Step 5: 研究參數化查詢及錯誤訊息處理方式，理解如何降低 SQL Injection 風險。

## 5. Initial Findings

| Test case                       | Observation                                       |
| ------------------------------- | ------------------------------------------------- |
| General invalid email           | HTTP 401                                          |
| Email containing a single quote | HTTP 500                                          |
| Error response                  | SQL syntax error reported                         |
| Source code                     | SQL query string directly interpolates user input |

## 6. Security Analysis

當使用者輸入直接串接到 SQL 查詢字串時，特殊字元可能改變查詢語法結構，形成 SQL Injection 風險。


## 7. Mitigation

* 使用參數化查詢，將 SQL 指令與使用者輸入分開處理。
* 避免將資料庫內部錯誤細節直接回傳給使用者。
* 保留適當的伺服器端日誌，以便診斷問題。

## 8. Limitations

目前已完成初步行為觀察與漏洞成因分析，尚未將登入繞過或未授權資料存取視為已驗證結果。

## 9. Learning Outcomes

學習到如何結合 HTTP 行為觀察與原始碼閱讀分析 Web 安全風險，也更理解參數化查詢在防禦 SQL Injection 中的作用。

## 10. References

* OWASP Juice Shop: https://github.com/juice-shop/juice-shop
* OWASP SQL Injection Prevention Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html
