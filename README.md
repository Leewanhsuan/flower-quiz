# 你是哪種花束？ — 花束人格測驗

回答 8 道情境題，找到最能代表你的花束人格。

## 7 種花束人格

| 花束 | 關鍵字 |
|------|--------|
| 蝴蝶蘭瀑布花束 | 儀式感、優雅、完美主義 |
| 鬱金香花束 | 全力綻放、熱情真實、活在當下 |
| 大地色混搭花束 | 審美主張強、不隨波逐流 |
| 冰島罌粟花束 | 獨立、感性、喜歡獨處 |
| 田園風格花束 | 自由隨性、不被定義 |
| 鈔票玫瑰花束 | 務實主義、直接、效益優先 |
| 街邊買的非洲菊 | 情感驅動、直接快樂、真誠 |

## Tech Stack

- 單一 HTML 檔案（HTML + CSS + JS）
- Vanilla JS，無框架
- Google Fonts（Cormorant Garamond + LXGW WenKai TC）
- html2canvas（結果截圖儲存）
- GA4 事件追蹤

## 檔案結構

```
index.html              ← 主檔案
assets/images/*.png     ← 7 種花束圖片
audio/bgm.mp3           ← 背景音樂
audio/pick.mp3          ← 選題音效
audio/result.mp3        ← 結果揭曉音效
```

## 部署

靜態網站，任何靜態託管皆可（Vercel / Netlify / GitHub Pages）。
