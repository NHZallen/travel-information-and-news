---
name: travel-information-and-news
description: Search and aggregate travel news, information, and reviews from multiple sources. Use when user asks about travel destinations, tourism news, hotel/attraction reviews, travel tips, or anything travel-related. Supports Tavily (required), Brave Search (optional), and browser-based scraping (optional) for sites like Xiaohongshu and X/Twitter.
---

# Travel Information and News

Aggregates travel news, destination info, and reviews from multiple sources.

## Quick Start

```bash
# Required: TAVILY_API_KEY in env or ~/.openclaw/.env
# Optional: BRAVE_API_KEY for Brave Search fallback

python scripts/search.py --query "Tokyo travel March 2026" --format text
python scripts/search.py --query "京都賞櫻推薦" --format pdf --output result.pdf
python scripts/search.py --query "Bali hotel reviews" --format docx --output result.docx
```

## Search Sources

| Source | Required | When Used |
|--------|----------|-----------|
| Tavily | ✅ Yes | Primary search for all queries |
| Brave Search | ❌ No | Fallback when Tavily results insufficient |
| Browser (Xvfb+Chromium+Puppeteer) | ❌ No | Sites Tavily/Brave can't reach (Xiaohongshu, X/Twitter, etc.) |

### Installing Optional Sources

**Brave Search:** Set `BRAVE_API_KEY` env var.

**Browser suite (三件套):** Requires three components working together:
- `Xvfb` — Virtual framebuffer (provides a fake display for Chromium)
- `Chromium` — Browser engine
- `Puppeteer` (Node.js) — Controls Chromium programmatically

Why not headless mode? Some websites block headless browsers. Running Chromium on a virtual display (Xvfb) makes it appear as a real browser, bypassing most detection.

Installation:
```bash
# Xvfb + Chromium
apt-get install -y xvfb chromium

# Puppeteer
npm install puppeteer
```

## Parameters

All parameters can be customized. Defaults are provided.

| Parameter | Default | Description |
|-----------|---------|-------------|
| `query` | *required* | Search query in any language |
| `time_range` | `pm` | Time filter: `pd`(24h), `pw`(week), `pm`(month), `py`(year), or custom |
| `region` | `ALL` | Region code: `ALL`, `US`, `CN`, `JP`, `TW`, etc. |
| `max_results` | unlimited | Limit number of results (0 = unlimited) |
| `format` | `text` | Output format: `text`, `docx`, `pdf` |
| `output` | stdout | Output file path |
| `use_brave` | `false` | Enable Brave Search fallback |
| `use_browser` | `false` | Enable browser scraping for blocked sites |
| `language` | auto | Output language (auto = follow query language) |

## Output Formats

- **text** — Plain text summary to stdout
- **docx** — Word document with structured sections
- **pdf** — PDF with Noto Sans SC font (supports CJK)

## Review Sources

When reviews are requested, the skill attempts to aggregate ratings from:
- TripAdvisor (via browser scraping)
- Google Maps / Google Reviews (via browser scraping)

## Workflow

1. Receive user query
2. Determine language from query
3. Search Tavily with query + parameters
4. If results insufficient → optionally try Brave Search
5. If specific sites blocked → optionally use browser suite
6. If reviews requested → aggregate ratings
7. Compile and deduplicate results
8. Format output (text / docx / pdf)

## Limits

- Browser suite requires ~512MB RAM for Xvfb + Chromium
- Review scraping depends on site structure (may break if sites change)
- Rate limits apply to Tavily and Brave APIs
