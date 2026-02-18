# 📋 Changelog / 開發日誌

本文件記錄 Sandrone Desktop Pet 的版本迭代歷程與故障排除紀錄。

---

## v4.0 — 語音 (TTS) 整合版 ✅ *（目前版本）*

### 新增
- `GradioTTSWorker`：連接 GPT-SoVITS，支援語音克隆合成
- `AudioPlayer`：獨立執行緒播放音訊，避免 UI 卡頓
- 深度思考模式 (`deep_mode`)：切換精簡 / 長文回答
- 前綴墊音機制，解決播放器吞字問題

### 修復
- 執行緒安全檢查：`isRunning()` + `terminate()` + `wait()`，根除 `QThread: Destroyed while running` 閃退
- `text_split_method="不切"`，修復長句被截斷問題

---

## v3.0 — 3D 動作整合版

### 新增
- `viewer.html` 與 Python 深度連動
- `play_motion()` / `play_sequence()` 情緒動作切換
- 20 種 VMD 動作支援

### 修復
- **物理引擎崩潰**：強制 `physics: false`
- **playAnimation 未定義**：在 `<head>` 預定義防呆空函數
- **Root Motion Fix**：過濾根骨骼 `.position` 軌道，防止模型跑出畫面
- **手動 Mixer 救援**：當 Helper 註冊失敗時，自動建立 `AnimationMixer`
- **中文路徑問題**：使用 `encodeURIComponent` 處理 VMD 檔名

---

## v2.0 — 動作與邏輯優化版

### 新增
- `OllamaWorker` 意圖判斷系統（天氣 / 搜尋 / 系統狀態）
- DuckDuckGo 網路搜尋整合
- 雙重人格系統（傲嬌研究者 / 病嬌被造物，各 50% 機率）
- 隨機待機動作（打哈欠、看旁邊、發呆）

---

## v1.0 — 基礎對話版

### 功能
- Ollama 文字對話
- 基礎天氣查詢（Open-Meteo API）
- PyQt6 透明懸浮視窗

---

## 🔮 未來版本規劃

### v5.0 — 網頁 / 手機端擴充版
- Flask + Ngrok 網頁穿透
- `mobile.html` 手機遠端連線
- Ngrok 403 / 白畫面問題已預研解決方案

### v6.0 — 視訊鏡頭整合版
- 攝影機表情辨識
- 根據使用者表情做出即時互動反應
- 視覺化情緒回饋系統
