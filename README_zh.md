# Travel Information and News

<p align="center">
  <strong>🌐 選擇語言 / Select Language / Выберите язык / اختر اللغة</strong>
</p>

<p align="center">
  <a href="README.md">English</a> ·
  <a href="#中文">中文</a> ·
  <a href="README_es.md">Español</a> ·
  <a href="README_ru.md">Русский</a> ·
  <a href="README_ar.md">العربية</a>
</p>

---

<a name="中文"></a>
## 🇹🇼 中文

一個 OpenClaw 技能，從多個來源聚合旅遊新聞、目的地資訊與評價。

### 功能特色

- 🔍 **多來源搜尋** — Tavily（必備）、Brave Search（選配）、瀏覽器爬取（選配）
- 🌐 **多語言** — 跟隨提問語言，可依要求切換
- 📄 **多種輸出格式** — 純文字、Word（docx）、PDF（支援中日韓字元）
- ⭐ **評價聚合** — TripAdvisor 與 Google Maps 評分（預設開啟，可關閉）
- 🧹 **去重** — 同次搜尋自動去除重複結果
- 📅 **時間篩選** — 24小時、一週、一個月、一年，或自訂範圍

### 環境需求

#### 必需
- Python 3.10+
- `requests` 套件
- **Tavily API key** — 免費申請：[tavily.com](https://tavily.com)

#### 選配
- **Brave Search API key** — 申請：[brave.com/search/api](https://brave.com/search/api)
- **Xvfb + Chromium + Puppeteer** — 用於爬取小紅書、X/Twitter 等網站

### 安裝

#### 1. 安裝 Python 套件

```bash
pip install requests fpdf2 python-docx
```

#### 2. 設定 API 金鑰

建立或編輯 `~/.openclaw/.env`：

```bash
TAVILY_API_KEY=你的_Tavily_金鑰
BRAVE_API_KEY=你的_Brave_金鑰    # 選配
```

#### 3.（選配）安裝瀏覽器套件

三件套由三個元件組成：
- **Xvfb** — 虛擬顯示器，預設解析度 1200x720x24
- **Chromium** — 瀏覽器引擎
- **Puppeteer**（Node.js）— 程式化控制 Chromium

為什麼不用 headless 模式？部分網站會偵測並阻擋 headless 瀏覽器。在虛擬顯示器上執行 Chromium 能讓它看起來像真實瀏覽器。

```bash
apt-get install -y xvfb chromium
npm install puppeteer
```

### 使用方式

#### 基本搜尋（純文字）

```bash
python scripts/search.py --query "東京旅遊攻略 2026"
```

#### 產生 PDF 報告

```bash
python scripts/search.py --query "京都賞櫻推薦" --format pdf --output kyoto.pdf
```

#### 產生 Word 文件

```bash
python scripts/search.py --query "峇里島住宿推薦" --format docx --output bali.docx
```

#### 關閉評價搜尋

```bash
python scripts/search.py --query "巴黎旅遊" --no_reviews
```

#### 時間範圍篩選

```bash
python scripts/search.py --query "旅遊新聞" --time_range pd   # 24小時內
python scripts/search.py --query "旅遊新聞" --time_range pw   # 一週內
python scripts/search.py --query "旅遊新聞" --time_range py   # 一年內
```

#### 啟用 Brave Search 備用

```bash
python scripts/search.py --query "京都秘境" --use_brave
```

#### 啟用瀏覽器爬取（小紅書、X 等）

```bash
python scripts/search.py --query "小紅書東京推薦" --use_browser
```

### 參數說明

| 參數 | 簡寫 | 預設值 | 說明 |
|------|------|--------|------|
| `--query` | `-q` | *必填* | 搜尋關鍵詞（任何語言） |
| `--time_range` | `-t` | `pm` | 時間範圍：`pd`(24h)、`pw`(週)、`pm`(月)、`py`(年) |
| `--region` | `-r` | `ALL` | 地區代碼：`ALL`、`US`、`CN`、`JP`、`TW` 等 |
| `--max_results` | `-n` | `0`（不限） | 結果數量上限 |
| `--format` | `-f` | `text` | 輸出格式：`text`、`docx`、`pdf` |
| `--output` | `-o` | 標準輸出 | 輸出檔案路徑 |
| `--use_brave` | | `false` | 啟用 Brave Search 備用 |
| `--use_browser` | | `false` | 啟用瀏覽器爬取 |
| `--no_reviews` | | `false` | 關閉評價搜尋（預設開啟） |
| `--language` | `-l` | 自動 | 輸出語言（自動=跟隨提問） |

### 授權

MIT

---

<p align="center">
  <a href="README.md">English</a> ·
  <a href="#中文">↑ 回到頂部</a> ·
  <a href="README_es.md">Español</a> ·
  <a href="README_ru.md">Русский</a> ·
  <a href="README_ar.md">العربية</a>
</p>
