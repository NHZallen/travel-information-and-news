# Travel Information and News

<p align="center">
  <strong>🌐 Выберите язык / Select Language / 選擇語言 / اختر اللغة</strong>
</p>

<p align="center">
  <a href="README.md">English</a> ·
  <a href="README_zh.md">中文</a> ·
  <a href="README_es.md">Español</a> ·
  <a href="#русский">Русский</a> ·
  <a href="README_ar.md">العربية</a>
</p>

---

<a name="русский"></a>
## 🇷🇺 Русский

Навык OpenClaw для агрегации новостей о путешествиях, информации о направлениях и отзывов из нескольких источников.

### Возможности

- 🔍 **Поиск из нескольких источников** — Tavily (обязательно), Brave Search (опционально), браузер (опционально)
- 🌐 **Мультиязычность** — Следует языку запроса, переключается по требованию
- 📄 **Несколько форматов вывода** — Текст, Word (docx), PDF (с поддержкой CJK)
- ⭐ **Агрегация отзывов** — Рейтинги TripAdvisor и Google Maps (включено по умолчанию, можно отключить)
- 🧹 **Дедупликация** — Автоматическое удаление дубликатов
- 📅 **Фильтр по времени** — 24ч, неделя, месяц, год или произвольный диапазон

### Требования

#### Обязательные
- Python 3.10+
- Пакет `requests`
- **API-ключ Tavily** — Бесплатно на [tavily.com](https://tavily.com)

#### Опциональные
- **API-ключ Brave Search** — На [brave.com/search/api](https://brave.com/search/api)
- **Xvfb + Chromium + Puppeteer** — Для сайтов вроде Xiaohongshu и X/Twitter

### Установка

```bash
pip install requests fpdf2 python-docx
```

Настройте API-ключи в `~/.openclaw/.env`:

```bash
TAVILY_API_KEY=ваш_ключ_tavily
BRAVE_API_KEY=ваш_ключ_brave    # Опционально
```

#### Набор браузера (опционально)

Набор браузера (三件套) использует три компонента:
- **Xvfb** — Виртуальный дисплей (разрешение по умолчанию: 1200x720x24)
- **Chromium** — Браузерный движок
- **Puppeteer** (Node.js) — Программное управление Chromium

```bash
apt-get install -y xvfb chromium
npm install puppeteer
```

### Использование

```bash
# Базовый поиск
python scripts/search.py --query "путешествие в Токио март 2026"

# Генерация PDF
python scripts/search.py --query "отели на Бали" --format pdf --output bali.pdf

# Генерация Word
python scripts/search.py --query "гид по Парижу" --format docx --output paris.docx

# Отключить отзывы
python scripts/search.py --query "поездка в Рим" --no_reviews

# Фильтр по времени
python scripts/search.py --query "новости путешествий" --time_range pw

# Включить Brave Search
python scripts/search.py --query "скрытые места Киото" --use_brave

# Включить браузер для заблокированных сайтов
python scripts/search.py --query "рекомендации путешествий" --use_browser
```

### Параметры

| Параметр | Сокр. | По умолчанию | Описание |
|----------|-------|--------------|----------|
| `--query` | `-q` | *обязательно* | Поисковый запрос (любой язык) |
| `--time_range` | `-t` | `pm` | Диапазон: `pd`(24ч), `pw`(неделя), `pm`(месяц), `py`(год) |
| `--region` | `-r` | `ALL` | Код региона |
| `--max_results` | `-n` | `0` (без лимита) | Лимит результатов |
| `--format` | `-f` | `text` | Формат: `text`, `docx`, `pdf` |
| `--output` | `-o` | stdout | Путь к файлу вывода |
| `--use_brave` | | `false` | Включить Brave Search |
| `--use_browser` | | `false` | Включить браузер |
| `--no_reviews` | | `false` | Отключить отзывы (включено по умолчанию) |
| `--language` | `-l` | auto | Язык вывода |

### Лицензия

MIT

---

<p align="center">
  <a href="README.md">English</a> ·
  <a href="README_zh.md">中文</a> ·
  <a href="README_es.md">Español</a> ·
  <a href="#русский">↑ Наверх</a> ·
  <a href="README_ar.md">العربية</a>
</p>
