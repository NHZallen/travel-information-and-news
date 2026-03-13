# Travel Information and News

<p align="center">
  <strong>🌐 Select Language / 選擇語言 / Выберите язык / اختر اللغة</strong>
</p>

<p align="center">
  <a href="../README.md">English</a> ·
  <a href="README_zh.md">中文</a> ·
  <a href="#español">Español</a> ·
  <a href="README_ru.md">Русский</a> ·
  <a href="README_ar.md">العربية</a>
</p>

---

<a name="español"></a>
## 🇪🇸 Español

Una habilidad de OpenClaw que agrega noticias de viajes, información de destinos y reseñas de múltiples fuentes.

### Características

- 🔍 **Búsqueda multi-fuente** — Tavily (requerido), Brave Search (opcional), navegador (opcional)
- 🌐 **Multi-idioma** — Sigue el idioma de la consulta, cambiable bajo demanda
- 📄 **Múltiples formatos** — Texto plano, Word (docx), PDF (con soporte CJK)
- ⭐ **Agregación de reseñas** — Calificaciones de TripAdvisor y Google Maps (activado por defecto, se puede desactivar)
- 🧹 **Deduplicación** — Elimina automáticamente resultados duplicados
- 📅 **Filtro de tiempo** — 24h, semana, mes, año o rango personalizado

### Requisitos

#### Requerido
- Python 3.10+
- Paquete `requests`
- **Clave API Tavily** — Gratis en [tavily.com](https://tavily.com)

#### Opcional
- **Clave API Brave Search** — En [brave.com/search/api](https://brave.com/search/api)
- **Xvfb + Chromium + Puppeteer** — Para sitios como Xiaohongshu y X/Twitter

### Instalación

```bash
pip install requests fpdf2 python-docx
```

Configure las claves API en `.env (in skill directory)`:

```bash
TAVILY_API_KEY=su_clave_tavily
BRAVE_API_KEY=su_clave_brave    # Opcional
```

#### Suite del navegador (opcional)

La suite del navegador (三件套) usa tres componentes:
- **Xvfb** — Framebuffer virtual (resolución predeterminada: 1200x720x24)
- **Chromium** — Motor del navegador
- **Puppeteer** (Node.js) — Controla Chromium programáticamente

```bash
apt-get install -y xvfb chromium
npm install puppeteer
```

### Uso

```bash
# Búsqueda básica
python scripts/search.py --query "viajes a Tokio marzo 2026"

# Generar PDF
python scripts/search.py --query "hoteles en Bali" --format pdf --output bali.pdf

# Generar Word
python scripts/search.py --query "guía de París" --format docx --output paris.docx

# Desactivar reseñas
python scripts/search.py --query "viajes a Roma" --no_reviews

# Filtro de tiempo
python scripts/search.py --query "noticias de viaje" --time_range pw

# Habilitar Brave Search
python scripts/search.py --query "joyas ocultas de Kioto" --use_brave

# Habilitar navegador para sitios bloqueados
python scripts/search.py --query "recomendaciones de viaje" --use_browser
```

### Parámetros

| Parámetro | Corto | Predeterminado | Descripción |
|-----------|-------|----------------|-------------|
| `--query` | `-q` | *requerido* | Consulta de búsqueda (cualquier idioma) |
| `--time_range` | `-t` | `pm` | Rango: `pd`(24h), `pw`(semana), `pm`(mes), `py`(año) |
| `--region` | `-r` | `ALL` | Código de región |
| `--max_results` | `-n` | `0` (sin límite) | Límite de resultados |
| `--format` | `-f` | `text` | Formato: `text`, `docx`, `pdf` |
| `--output` | `-o` | stdout | Ruta del archivo de salida |
| `--use_brave` | | `false` | Habilitar Brave Search |
| `--use_browser` | | `false` | Habilitar navegador |
| `--no_reviews` | | `false` | Desactivar reseñas (activado por defecto) |
| `--language` | `-l` | auto | Idioma de salida |

### Licencia

MIT

---

<p align="center">
  <a href="../README.md">English</a> ·
  <a href="README_zh.md">中文</a> ·
  <a href="#español">↑ Volver arriba</a> ·
  <a href="README_ru.md">Русский</a> ·
  <a href="README_ar.md">العربية</a>
</p>
