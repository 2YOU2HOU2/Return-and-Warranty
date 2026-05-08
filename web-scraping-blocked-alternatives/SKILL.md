---
name: web-scraping-blocked-alternatives
description: Legitimate alternatives when websites with enterprise-grade anti-bot protection block automation. Covers detection patterns, alternative data sources, and ethical approaches.
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [web-scraping, bot-detection, alternatives, real-estate, blocked]
    related_skills: []
---

# Web Scraping Blocked - Alternative Approaches

## When to Use

Websites with enterprise-grade anti-bot protection (Akamai, CloudFront, KPSDK) actively block browser automation. This skill documents legitimate alternatives when direct scraping fails.

## Detection Patterns

These indicate server-level blocking that cannot be bypassed:

1. **Realtor.com pattern**: Status 429 or 403 with "Your request could not be processed"
   - Reference IDs change on each attempt (active blocking)
   - No CAPTCHA or interactive challenge - just a hard block
   - Contact email like `unblockrequest@realtor.com`

2. **CloudFront/Akamai errors**: "403 ERROR" with cloudfront.net request IDs

3. **"Are You a Robot?" pages**: With rate limiting algorithm messages

4. **"Press & Hold to confirm you are a human"**: Interactive challenges

5. **KPSDK JavaScript**: `window.KPSDK` in page source indicates Kasada protection

## Alternative Approaches

### Option 1: Text Extraction Services

Services that may have cached or authorized access:

```
https://r.jina.ai/http://example.com
https://r.jina.ai/http://cc.bingj.com/cache.aspx?d=DOC_ID&u=URL
https://webcache.googleusercontent.com/search?q=URL
```

**Limitation**: If source blocks everyone, these also fail. Good for simple sites, not enterprise-protected ones.

### Option 2: Official APIs

Many sites offer legitimate APIs:

- **Realtor.com**: Has partner/developer APIs (requires registration)
- **Zillow**: Zillow API Network (paid tiers available)
- **Redfin**: Limited public data center

Search for `<site> developer API` before attempting scraping.

### Option 3: Public/Open Data Sources

For real estate specifically:

- **Chicago Data Portal** (data.cityofchicago.org): Property, permit, ownership data
- **Cook County Recorder**: Property tax records
- **City Assessor Databases**: Many cities provide bulk data downloads
- **Third-party services**: ATTOM Data, CoreLogic (paid but legitimate)

### Option 4: Manual Transfer

When automation completely fails:

1. User visits site directly in their browser
2. Copies listing/page data
3. Pastes into conversation
4. AI formats into tables/structured data

**Advantage**: Fastest when all automation routes are blocked.

## Known Blocking Sites

| Site | Block Type | Notes |
|------|-----------|-------|
| Realtor.com | Server-side IP block | Akamai/CloudFront, KPSDK protection |
| Redfin | Rate limit + detection | "Are you a robot" after first request |
| Zillow | Interactive challenge | "Press & Hold" widget |
| Homes.com | Akamai Access Denied | Edge server blocking |

## What NOT to Do

- **Don't research bypass techniques** - Violates Terms of Service, ethical concerns
- **Don't attempt to defeat KPSDK** or anti-bot JavaScript challenges
- **Don't use residential proxies** to circumvent blocks
- **Don't teach or document circumvention methods**

Enterprise protection (Akamai, Kasada, CloudFront) blocks at infrastructure level before JavaScript. No "stealth" will help - these are designed to stop automation.

## Recommended Response

When blocked, be transparent:

```
"The site uses Akamai/CloudFront enterprise blocking that I cannot bypass 
for ethical and technical reasons. The protection is server-level, not 
a solvable CAPTCHA. Here are legitimate alternatives..."
```

Then provide:
1. **Manual option**: User copies data, you format it
2. **Alternative sources**: Official APIs, open data portals
3. **Timeline**: If it's a temporary rate limit, suggest waiting

## Key Insight

The presence of `unblockrequest@domain.com` emails and changing reference IDs indicates **intentional blocking of all automation**, not a temporary issue. Don't keep retrying - pivot to alternatives immediately.

## Example Usage

User: "Scrape data from enterprise-protected site"

Assistant: 
1. Detect blocking pattern (429, reference IDs, error messages)
2. Stop after 2-3 attempts max
3. Explain the blocking is intentional/server-level
4. Offer: Manual transfer, official APIs, or public data sources
5. Never suggest or research bypass methods