# Travel Information and News

<p dir="rtl" align="center">
  <strong>🌐 اختر اللغة / Select Language / 選擇語言 / Выберите язык</strong>
</p>

<p align="center">
  <a href="README.md">English</a> ·
  <a href="README_zh.md">中文</a> ·
  <a href="README_es.md">Español</a> ·
  <a href="README_ru.md">Русский</a> ·
  <a href="#العربية">العربية</a>
</p>

---

<a name="العربية"></a>
## 🇸🇦 العربية

أداة OpenClaw لتجميع أخبار السفر ومعلومات الوجهات والمراجعات من مصادر متعددة.

### المميزات

- 🔍 **بحث متعدد المصادر** — Tavily (مطلوب)، Brave Search (اختياري)، متصفح (اختياري)
- 🌐 **متعدد اللغات** — يتبع لغة الاستعلام، قابل للتبديل
- 📄 **صيغ إخراج متعددة** — نص عادي، Word (docx)، PDF (يدعم CJK)
- ⭐ **تجميع المراجعات** — تقييمات TripAdvisor و Google Maps (مفعّل افتراضياً، يمكن تعطيله)
- 🧹 **إزالة المكررات** — إزالة تلقائية للنتائج المكررة
- 📅 **تصفية زمنية** — 24 ساعة، أسبوع، شهر، سنة أو نطاق مخصص

### المتطلبات

#### مطلوب
- Python 3.10+
- حزمة `requests`
- **مفتاح Tavily API** — مجاني على [tavily.com](https://tavily.com)

#### اختياري
- **مفتاح Brave Search API** — من [brave.com/search/api](https://brave.com/search/api)
- **Xvfb + Chromium + Puppeteer** — لمواقع مثل Xiaohongshu و X/Twitter

### التثبيت

```bash
pip install requests fpdf2 python-docx
```

قم بإعداد مفاتيح API في `~/.openclaw/.env`:

```bash
TAVILY_API_KEY=مفتاح_Tavily_الخاص_بك
BRAVE_API_KEY=مفتاح_Brave_الخاص_بك    # اختياري
```

#### حزمة المتصفح (اختياري)

تتكون من ثلاثة مكونات:
- **Xvfb** — شاشة افتراضية (الدقة الافتراضية: 1200x720x24)
- **Chromium** — محرك المتصفح
- **Puppeteer** (Node.js) — التحكم في Chromium برمجياً

```bash
apt-get install -y xvfb chromium
npm install puppeteer
```

### الاستخدام

```bash
# بحث أساسي
python scripts/search.py --query "رحلة إلى طوكيو مارس 2026"

# إنشاء PDF
python scripts/search.py --query "فنادق بالي" --format pdf --output bali.pdf

# إنشاء Word
python scripts/search.py --query "دليل باريس" --format docx --output paris.docx

# تعطيل المراجعات
python scripts/search.py --query "رحلة إلى روما" --no_reviews

# تصفية زمنية
python scripts/search.py --query "أخبار السفر" --time_range pw

# تفعيل Brave Search
python scripts/search.py --query "أماكن خفية في كيوتو" --use_brave

# تفعيل المتصفح للمواقع المحجوبة
python scripts/search.py --query "توصيات السفر" --use_browser
```

### المعاملات

| المعامل | اختصار | الافتراضي | الوصف |
|---------|--------|-----------|-------|
| `--query` | `-q` | *مطلوب* | استعلام البحث (أي لغة) |
| `--time_range` | `-t` | `pm` | النطاق: `pd`(24س)، `pw`(أسبوع)، `pm`(شهر)، `py`(سنة) |
| `--region` | `-r` | `ALL` | رمز المنطقة |
| `--max_results` | `-n` | `0` (بدون حد) | حد النتائج |
| `--format` | `-f` | `text` | الصيغة: `text`، `docx`، `pdf` |
| `--output` | `-o` | stdout | مسار ملف الإخراج |
| `--use_brave` | | `false` | تفعيل Brave Search |
| `--use_browser` | | `false` | تفعيل المتصفح |
| `--no_reviews` | | `false` | تعطيل المراجعات (مفعّل افتراضياً) |
| `--language` | `-l` | auto | لغة الإخراج |

### الترخيص

MIT

---

<p align="center">
  <a href="README.md">English</a> ·
  <a href="README_zh.md">中文</a> ·
  <a href="README_es.md">Español</a> ·
  <a href="README_ru.md">Русский</a> ·
  <a href="#العربية">↑ العودة للأعلى</a>
</p>
