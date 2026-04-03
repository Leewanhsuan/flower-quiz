# Flower Personality Quiz

## Overview
Single-page 花束人格測驗網站，使用者回答 8 題情境題後，得到 7 種花束人格之一的結果，可分享或儲存結果圖。

## Tech Stack
- **單一 HTML 檔案**：所有 CSS、JS、資料都內嵌於 `flower-personality-quiz.html`
- **純 Vanilla JS**，無框架
- **外部依賴**：
  - Google Fonts（Cormorant Garamond + Noto Serif TC）
  - html2canvas 1.4.1（CDN）— 用於儲存結果截圖
  - Google Analytics 4（Measurement ID: `G-ZQV7NGH95H`）

## File Structure
```
flower-personality-quiz.html   ← 唯一主檔案（HTML + CSS + JS）
audio/bgm.mp3                 ← 背景音樂
audio/pick.mp3                ← 選題音效
audio/result.mp3              ← 結果揭曉音效
```

## Architecture (within the HTML file)

### CSS (line 8–616)
- CSS 變數定義於 `:root`，包括色彩 token 與每種花束的 accent color
- 響應式設計：480px breakpoint

### HTML (line 627–760)
- `#start-screen` → 開始畫面
- `#quiz-screen` → 題目畫面（含進度條）
- `#result-screen` → 結果畫面（含優勢/盲點/搭配）
- `#share-overlay` → 分享 modal（LINE / IG / FB / 複製連結）
- `#save-card` → 截圖用隱藏卡片（html2canvas 目標）

### JS Data (line 773–993)
- `FLOWERS` 物件：7 種花束人格定義（id, icon, name, latin, tagline, traits, desc, strength, blind, compat）
- `QUESTIONS` 陣列：8 題，每個選項帶 `weights` 對應花束 key 的加權分數

### JS Logic (line 995+)
- **計分方式**：每選一個選項，累加該選項 `weights` 中各花束的分數，最後取最高分者
- **選項順序**：每次測驗會 shuffle 選項順序
- **分享**：手機優先用 `navigator.share`，桌機用自訂 modal
- **儲存**：將結果填入隱藏 `#save-card`，用 html2canvas 截圖後觸發下載

### GA4 Events
| Event | Trigger | Extra Params |
|-------|---------|--------------|
| `quiz_start` | 點「開始測驗」 | — |
| `quiz_complete` | 完成測驗看到結果 | `result_bouquet`, `result_name` |
| `share_open` | 點分享按鈕 | `result_name` |
| `share` | 選擇分享平台 | `platform` |
| `save_card` | 儲存結果圖片 | `result_name` |

### 7 Flower Types (keys)
`cascade`(蝴蝶蘭瀑布花束), `tulip`(鬱金香花束), `editorial`(大地色混搭花束), `poppy`(單支冰島罌粟), `wild`(Garden Style 野花束), `rose`(鈔票玫瑰束), `market`(街邊非洲菊)

## Common Update Tasks
- **改題目/選項**：編輯 `QUESTIONS` 陣列，每個選項的 `weights` 決定計分
- **改花束結果文案**：編輯 `FLOWERS` 物件中對應 key 的欄位
- **加新花束**：在 `FLOWERS` 加新 key，在 `scores` 初始值加對應 key，並在題目 weights 中加入權重
- **改分享文案**：搜尋 `openShare` 函數中的 `_shareText`
- **改 GA4 Measurement ID**：搜尋 `G-ZQV7NGH95H` 替換
- **改音效/音樂**：替換 `audio/` 資料夾中的檔案
