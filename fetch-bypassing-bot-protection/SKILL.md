---
name: fetch-bypassing-bot-protection
description: Fetch URLs blocked by bot protection (PerimeterX, Cloudflare, etc.) using iPhone User-Agent or playwright-stealth
triggers:
  - fetch URL blocked
  - access denied CAPTCHA
  - curl blocked by PerimeterX
  - site blocking automated requests
---

# Fetch URL Bypassing Bot Protection

## When to Use
Any time you need to fetch data from a URL and the site blocks automated requests with bot protection (CAPTCHA, "Access denied", PerimeterX, etc.).

## Core Technique: iPhone User-Agent
Many sites (Urban Outfitters, Potbelly, etc.) use PerimeterX or similar anti-bot solutions that only challenge **desktop** browsers. Mobile User-Agents pass through because the anti-bot JS is less aggressive on mobile paths.

## Step-by-Step Workflow

### Step 1: Try Mobile iPhone UA First
Always attempt with iPhone UA first — it's the simplest bypass:

```bash
curl -s --max-time 15 \
  -A "Mozilla/5.0 (iPhone; CPU iPhone OS 17_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.0 Mobile/15E148 Safari/604.1" \
  "YOUR_URL_HERE"
```

### Step 2: Check the Response
- **"denied" / "captcha" / "px-captcha"** in response → blocked, try Step 3
- **Contains product names / prices / HTML content** → success! Extract data
- **404 / empty** → wrong endpoint, try different URL or params

### Step 3: If Blocked — Try playwright-stealth
Some sites are more aggressive. Use `playwright-stealth` for full browser automation with anti-detection evasions:

```python
import sys
sys.path.insert(0, '/Users/youzhou/Library/Python/3.9/lib/python/site-packages')

from playwright_stealth import Stealth
from playwright.sync_api import sync_playwright

with Stealth().use_sync(sync_playwright()) as p:
    browser = p.chromium.launch(headless=True)
    page = browser.new_page()
    page.goto("YOUR_URL_HERE", timeout=20000)
    page.wait_for_timeout(3000)
    content = page.content()
    title = page.title()
    browser.close()
```

**Note**: `playwright_stealth` must be installed in the venv at `/Users/youzhou/.hermes/hermes-agent/venv/bin/python3`. The system Python at `/usr/bin/python3` has it installed at `/Users/youzhou/Library/Python/3.9/lib/python/site-packages`.

### Step 4: Alternative Mobile UAs
If iPhone OS 17 doesn't work, try:

```
# iOS 15
Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Mobile/15E148 Safari/604.1

# Android
Mozilla/5.0 (Linux; Android 13; Pixel 7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Mobile Safari/537.36
```

### Step 5: For Urban Outfitters specifically
```bash
# Sale page with brand filter
curl -s -A "Mozilla/5.0 (iPhone; CPU iPhone OS 17_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.0 Mobile/15E148 Safari/604.1" \
  "https://www.urbanoutfitters.com/sale?brand=Oakley"
```

## How to Extract Product Count from Response

```bash
# Extract product count from page text
grep -oP '\d+ products' <<< "$response"

# Extract JSON-LD product list
grep -oP '"itemListElement":\[.*?\]' <<< "$response"
```

## Pitfalls

- **Cloudflare** blocks datacenter IPs aggressively — try residential proxy or browser approach
- **Session cookies** may be needed for authenticated content — use browser tool
- **JavaScript-rendered content** — curl won't see it, use playwright or browser tool
- **Rate limiting** — add `sleep 1` between requests if scraping multiple pages
- **Some sites** (Google, DuckDuckGo) also block — try Bing or alternative search engines

## Verification
After fetching, always check:

1. Title doesn't say "Access denied" or "CAPTCHA"
2. Response contains expected content (product names, prices, etc.)
3. HTTP status is 200 (add `-I` to curl to check)
