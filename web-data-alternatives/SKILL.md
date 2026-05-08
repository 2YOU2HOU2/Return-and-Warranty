---
name: web-data-alternatives
description: Find alternative data sources when websites block automated scraping with bot detection
trigger:
  - website blocks automated access
  - bot detection prevents data extraction
  - need data from protected real estate/travel sites
  - scraping returns security/block pages
  - real estate data access blocked
  - flight data access blocked
  - enterprise bot protection encountered
---

# Web Data Alternatives When Sites Block Scraping

## Problem
Many websites (especially real estate, travel, e-commerce) use enterprise-grade bot protection:
- CDN-level blocking (CloudFront, Akamai)
- JavaScript challenges (KPSDK scripts)
- Browser fingerprinting
- Rate limiting by IP
- HeadlessChrome detection

## Solution: Accept Block, Find Alternatives

### Step 1: Don't Try to Bypass
Bypassing violates ToS and security infrastructure. Instead, find legitimate alternatives.

### Step 2: Try these Alternative Sources

**Real Estate Data:**
- MLS foreclosure sites (mls.foreclosure.com) - less protected
- City Data Portals - data.cityofchicago.org
- Public property records - Cook County
- Redfin Data Center - CSV downloads
- Zillow Research - datasets available

**Travel/Flight Data:**
- ITA Matrix (matrix.itasoftware.com) - Google's backend
- Individual airline sites directly
- Historical data patterns
- Manual search on user's device

**General Alternatives:**
- Text extraction: r.jina.ai/http://URL
- Cached pages: textise dot iitty via r.jina.ai
- Bing/Google cached pages
- Public APIs if available

### Step 3: Ethical Boundaries

**DO NOT:**
- Use residential proxies
- Circumvent protections
- Defeat CAPTCHA
- Violate ToS

**DO:**
- Try public text extraction services
- Check government/open data sources
- Use official APIs when available
- Ask user to manually extract data for formatting

### Step 4: When Completely Blocked

1. Explain the blocking clearly
2. Offer to format manual data
3. Suggest alternative legitimate methods
4. Don't persist with workarounds

## Known Protected Sites:

**Real Estate:** Realtor.com, Zillow, Redfin, Trulia
**Travel:** Expedia, Skyscanner, Kayak, airline booking
**Financial:** Banking/investment sites

## Sites That Usually Allow Access:

- Government/open data portals
- Industry-specific aggregators
- Cached/text extraction services
- ITA Matrix (flight data)
- Some MLS foreclosure sites

## Example Test Code:

```python
import requests

# Test text extraction
url = 'https://r.jina.ai/http://example.com'
try:
    response = requests.get(url, timeout=30)
    if response.status_code == 200:
        data = response.text
except:
    print("Blocked")
```

## Real-World Finding:

In this conversation, Realtor.com blocked all access (CloudFront 429 errors, KPSDK challenges). However, mls.foreclosure.com loaded successfully and provided 28,997 Chicago foreclosure listings when the main site was inaccessible.

Similarly, Google Flights showed cached data but wouldn't load real-time results, and flight booking sites (Skyscanner, Expedia, airline sites) all showed bot detection pages.