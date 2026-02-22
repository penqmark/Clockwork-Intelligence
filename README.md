# 🎭 Sandrone Desktop Pet — AI 桌面寵物

<div align="center">

**一個擁有 3D MMD 模型、雙重人格、語音合成的 AI 桌面寵物**

*An AI Desktop Pet with 3D MMD Model, Dual Personality & Voice Synthesis*

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)](https://python.org)
[![PyQt6](https://img.shields.io/badge/PyQt6-6.5+-41CD52?logo=qt&logoColor=white)](https://www.riverbankcomputing.com/software/pyqt/)
[![Ollama](https://img.shields.io/badge/Ollama-Local_LLM-000000?logo=ollama)](https://ollama.com)
[![Three.js](https://img.shields.io/badge/Three.js-r160-000000?logo=threedotjs)](https://threejs.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

</div>

---

## 📖 簡介 | About

**Sandrone** 是一個以《原神》愚人眾執行官「桑多涅」為角色原型的 AI 桌面寵物。她不只是一個聊天視窗——她是一個活在你桌面上、擁有 3D 動作、會說話、有脾氣的 AI 夥伴。

本專案整合了 **本地 LLM 推理（Ollama）**、**3D MMD 模型渲染（Three.js）**、**語音合成（GPT-SoVITS）**，並透過 **PyQt6** 打造成一個透明懸浮的桌面應用。

> **⚡ 當前版本：v4.0（桌面端）**
>
> 下一代 **v5.0** 將加入 **Flask + Ngrok 網頁遠端控制**（含手機端 `mobile.html`），敬請期待！
>
> **未來規劃** 還包括 **視訊鏡頭整合**，讓 Sandrone 能看見你、辨識表情並做出互動反應。

---

## ✨ 功能特色 | Features

### 🧠 AI 對話引擎
- 基於 **Ollama** 本地 LLM（支援 Llama3、Mistral 等模型）
- **雙重人格系統**：50% 機率切換「傲嬌毒舌研究者」或「病嬌被造物」模式
- **深度思考模式**：可切換精簡對話 / 長文深度回答
- **意圖判斷**：自動識別天氣查詢、系統狀態、網路搜尋等需求

### 🎭 3D 模型與動作
- 使用 **Three.js + MMDLoader** 載入 PMX 模型
- **20+ 種動作**：待機、問候、思考、生氣、跳舞等
- **Root Motion Fix**：過濾根骨骼位移，防止模型飛出畫面
- **隨機待機行為**：定時觸發打哈欠、看旁邊、發呆等動作

### 🔊 語音合成（TTS）
- 整合 **GPT-SoVITS** 語音克隆
- 支援情感語音生成
- 獨立執行緒播放，不卡 UI

### 🛠️ 實用工具
- **天氣查詢**（Open-Meteo API，支援全台灣地名）
- **系統監控**（CPU / 記憶體 / 電池）
- **網路搜尋**（DuckDuckGo）

### 🎨 介面設計
- 透明懸浮視窗，桌面寵物體驗
- 深色 / 淺色主題切換
- 懸浮模式（純文字無邊框）
- 可拖曳、右鍵選單、對話紀錄自動存檔

---

## 🏗️ 專案結構 | Project Structure

```
sandrone-desktop-pet/
├── main.py              # 🐍 Python 主程式（UI + AI + TTS）
├── viewer.html          # 🌐 3D 模型渲染頁面（Three.js）
├── ref.wav              # 🔊 TTS 參考音訊（需自行準備）
├── requirements.txt     # 📦 Python 依賴
├── .gitignore
├── LICENSE
├── README.md
├── model/               # 📁 MMD 模型資料夾（需自行放入）
│   ├── model.pmx
│   └── (材質貼圖...)
├── motions/             # 📁 VMD 動作檔案（原創，已包含）
│   ├── Idle_Stable_01.vmd
│   ├── Start_Init_01.vmd
│   └── ...（共 20 個動作檔）
└── versions/            # 📂 歷史版本存檔
    ├── v1.0/main_v1.py
    ├── v2.0/main_v2.py
    └── v3.0/main_v3.py + viewer_v3.html
```

> ⚠️ `model/` 資料夾內的模型檔案因版權問題不包含在此 repo 中，請自行準備 MMD 模型。
>
> ✅ `motions/` 內的動作檔案為本專案原創製作，已包含在 repo 中。但不同模型的骨骼結構可能不同，若動作異常請參考下方的「模型相容性」說明。

### 🎮 模型哪裡找？| Where to Get Models

本專案支援任何標準 **MMD PMX 格式**的模型，你可以自由替換成喜歡的角色！

| 來源 | 說明 | 連結 |
|------|------|------|
| **模之屋 (Aplaybox)** | miHoYo 官方合作平台，提供原神、崩壞等角色的 MMD 模型 | [aplaybox.com](https://www.aplaybox.com) |
| **Bowlroll** | 日本最大 MMD 資源站，大量高品質模型 | [bowlroll.net](https://bowlroll.net) |
| **DeviantArt** | 國際社群，搜尋 "MMD model download" | [deviantart.com](https://www.deviantart.com) |
| **自製模型** | 使用 PMX Editor 或 Blender + MMD Tools 自製 | — |

**使用方式：** 下載後將 `.pmx` 檔案重新命名為 `model.pmx`，連同所有材質貼圖一起放入 `model/` 資料夾即可。

### ⚡ 模型相容性注意事項 | Model Compatibility

本專案附帶的 VMD 動作檔案是**原創製作**的，不存在版權問題。但由於不同 MMD 模型的骨骼結構可能有差異，替換模型後可能會遇到以下狀況：

| 現象 | 原因 | 解法 |
|------|------|------|
| 部分動作不自然 / 肢體扭曲 | 模型骨骼命名或結構與動作檔不匹配 | 使用 PMX Editor 確認骨骼名稱是否為日文標準命名 |
| 模型做動作後位移 / 飄走 | 模型的根骨骼名稱不在過濾清單內 | 修改 `viewer.html` 中 Root Motion Fix 的骨骼過濾正則表達式 |
| 動作完全不播放 | 模型缺少對應的骨骼 | 選用骨骼結構較完整的模型，或用 PMX Editor 補齊缺失骨骼 |

> 💡 **建議**：動作檔案基於常見的日文標準骨骼命名（センター、全ての親 等）製作。選擇模型時，優先挑選骨骼結構完整且使用日文標準命名的模型，相容性最佳。

---

## 🚀 安裝與執行 | Setup

### 前置需求

| 工具 | 用途 | 下載連結 |
|------|------|----------|
| **Python 3.10+** | 執行主程式 | [python.org](https://python.org) |
| **Ollama** | 本地 LLM 推理 | [ollama.com](https://ollama.com) |
| **GPT-SoVITS** | 語音合成（選用） | [GitHub](https://github.com/RVC-Boss/GPT-SoVITS) |

### 步驟

```bash
# 1. Clone 專案
git clone https://github.com/YOUR_USERNAME/sandrone-desktop-pet.git
cd sandrone-desktop-pet

# 2. 安裝 Python 依賴
pip install -r requirements.txt

# 3. 啟動 Ollama 並下載模型
ollama pull llama3

# 4. 準備 MMD 模型
#    將 .pmx 模型放入 model/ 資料夾
#    將 .vmd 動作放入 motions/ 資料夾

# 5. （選用）啟動 GPT-SoVITS WebUI
#    確保運行在 http://localhost:9872/
#    準備 ref.wav 參考音訊

# 6. 啟動！
python main.py
```

---

## ⚙️ 設定說明 | Configuration

`main.py` 頂部的配置區可自訂：

```python
# TTS 後台網址
GRADIO_URL = "http://localhost:9872/"

# 參考音訊（TTS 音色克隆用）
REF_AUDIO_PATH = "ref.wav"
REF_TEXT = "這就是你要的數據嗎？"

# 氣泡框尺寸
BUBBLE_MIN_WIDTH = 120
BUBBLE_MAX_WIDTH = 280
BUBBLE_MAX_HEIGHT = 450
```

右鍵點擊模型 → **設定** 可調整：
- LLM 模型選擇
- 深色 / 淺色主題
- 懸浮模式開關
- 深度思考模式
- 人格 Prompt 自訂

---

## 🎭 自訂人格 | Personality Customization

想讓你的桌面寵物擁有獨特的性格？有 **兩種方式** 可以修改：

### 方式一：設定面板（快速調整）

右鍵點擊模型 → **設定** → 最下方的「**人格設定**」文字框，直接輸入你想要的性格描述，例如：

```
妳是一個活潑開朗的貓娘，喜歡用「喵～」結尾，對主人非常撒嬌。
```

這個方式適合 **即時測試不同風格**，重啟程式後會恢復預設。

### 方式二：修改原始碼（永久生效）

打開 `main.py`，找到以下兩個區塊進行修改：

**1. 基礎人格（約第 314 行）**
```python
self.current_personality = "妳優雅、理性。妳視使用者為合作夥伴。"
```
改成你想要的基礎性格設定。

**2. 雙重人格 Prompt（約第 196~218 行）**

這裡控制了兩種人格的切換邏輯，你可以自由修改：

```python
# 模式 A：傲嬌毒舌（50% 機率觸發）
if dice > 0.5:
    persona = (
        "【當前模式：傲慢的研究者】\n"
        "1. **語氣**：挑剔、專業、冷淡。\n"
        # ... 自由修改 ...
    )
# 模式 B：病嬌被造物（50% 機率觸發）
else:
    persona = (
        "【狀態：核心權限已開放】\n"
        "1. **語氣**：極度甜美、黏人、順從。\n"
        # ... 自由修改 ...
    )
```

> 💡 **進階玩法**：你也可以調整 `dice > 0.5` 的數值來改變兩種人格的出現機率，例如改成 `dice > 0.3` 就會有 70% 的機率觸發模式 B。

---

## 🗺️ 開發藍圖 | Roadmap

- [x] **v1.0** — 基礎 Ollama 文字對話一鍵下載|(https://github.com/penqmark/Ollama-Flow-Commander)
- [x] **v2.0** — 2D形象及天氣,電腦狀態,搜尋系統|(https://github.com/penqmark/SystemSoul)
- [x] **v3.0** — 3D MMD 模型動作整合
- [x] **v3.1** — 意圖判斷 + 雙重人格 + 搜尋功能(優化)
- [x] **v4.0** — GPT-SoVITS 語音合成 ← *（目前版本）*
- [ ] **v5.0** — Flask + Ngrok 網頁端 & 手機遠端控制
- [ ] **v6.0** — 視訊鏡頭整合（表情辨識 & 互動反應）

---

## 🐛 已知問題與故障排除 | Troubleshooting

<details>
<summary><b>🔧 環境與依賴</b></summary>

| 問題 | 原因 | 解法 |
|------|------|------|
| `ModuleNotFoundError` | 套件安裝到錯誤的 Python 環境 | 使用 `python -m pip install -r requirements.txt` |
| `NameError: BUBBLE_MAX_WIDTH` | 複製代碼時遺漏配置區 | 確認 `main.py` 頂部配置區完整 |

</details>

<details>
<summary><b>🎭 3D 模型與動畫</b></summary>

| 問題 | 原因 | 解法 |
|------|------|------|
| 模型全黑 / 載入失敗 | `physics: true` 在本地環境無法載入 `ammo.wasm` | 已強制 `physics: false` |
| `playAnimation is not defined` | Python 指令比網頁載入更快 | 已在 `<head>` 加入防呆空函數 |
| 模型做動作後消失 | VMD 包含根骨骼位移 | 已加入 Root Motion Fix 過濾 `.position` 軌道 |
| `Failed to fetch` 動作檔 | 中文檔名編碼問題 | 使用 `encodeURIComponent` 處理 |

</details>

<details>
<summary><b>🔊 語音合成 (TTS)</b></summary>

| 問題 | 原因 | 解法 |
|------|------|------|
| `Connection refused` | GPT-SoVITS 未啟動或端口不對 | 確認 WebUI 在 `localhost:9872` |
| 聲音開頭被切掉 | 播放器啟動延遲 | 已加入前綴墊音 |
| 沒有聲音 / 無情感 | `ref.wav` 路徑錯誤 | 確認專案根目錄有 `ref.wav` |

</details>

<details>
<summary><b>💥 程式崩潰</b></summary>

| 問題 | 原因 | 解法 |
|------|------|------|
| `QThread: Destroyed while running` | 新執行緒覆蓋未結束的舊執行緒 | 已加入 `isRunning()` 安全檢查 |
| 輸入後直接閃退 | 變數未定義或路徑錯誤 | 檢查終端機錯誤訊息 |

</details>

---

## 📂 歷史版本 | Version Archive

`versions/` 資料夾保存了各版本的程式碼，展示專案演進過程：

| 版本 | 說明 | 檔案 |
|------|------|------|
| v1.0 | 基礎對話（Ollama + 天氣） | `versions/v1.0/main_v1.py` |
| v2.0 | 意圖判斷 + 雙重人格 + 搜尋 | `versions/v2.0/main_v2.py` |
| v3.0 | 3D 模型動作整合 | `versions/v3.0/main_v3.py` + `viewer_v3.html` |
| v4.0 | TTS 語音 + 深度思考 + 網路地理位置判斷| 根目錄 `main.py`（目前版本） |

---

## 🤝 貢獻 | Contributing

歡迎提交 Issue 和 Pull Request！如果你有：
- 更好的 VMD 動作檔案
- 其他 LLM / TTS 後端的整合方案
- 跨平台適配（目前音訊播放使用 macOS 的 `afplay`）

都非常歡迎一起開發。

---

## 📜 授權 | License

本專案以 [MIT License](LICENSE) 釋出。

MMD 模型檔案版權歸原作者所有，請遵守各自的使用條款。動作檔案（`.vmd`）為本專案原創，隨 MIT 授權釋出。

---

<div align="center">

*「這就是你寫的代碼？……算了，看在你是我維護者的份上。」 —— Sandrone*

</div>
