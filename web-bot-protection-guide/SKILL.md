---
name: web-bot-protection-guide
tags: [web-scraping, bot-detection, anti-bot, blocked-sites, alternatives]
description: Reference guide for sites with aggressive anti-bot protections and viable alternatives
---

# Bot Protection Site Guide

## Sites with Enterprise-Grade Blocking (Access Denied)

### Real Estate
| Site | Protection | Status |
|------|------------|--------|
| **Realtor.com** | CloudFront CDN | ❌ Blocked before HTML |
| **Zillow** | CloudFront + challenge | ❌ "Press & Hold" required |
| **Redfin** | Rate limiting | ❌ 429 errors |
| **Trulia** | CloudFront | ❌ Blocked |
| **Homes.com** | Akamai | ❌ Access Denied |
| **Cook County** | CloudFront | ❌ Blocked |

**Alternatives:**
- MLS.foreclosure.com - Works for foreclosure data
- Chicago Data Portal - Limited property data
- Manual extraction only option for clean listings

### Other High-Protection Categories
- Major airlines (some rate limit)
- LinkedIn
- Most social media platforms
- Government databases with restrictions

## Automation-Friendly Sites

### Travel/Flights
| Site | Status | Notes |
|------|--------|-------|
| **Google Flights** | ✅ Works | Fully accessible |
| **Expedia** | ⚠️ Limited | May require CAPTCHA |
| **Kayak** | ⚠️ Limited | Varies |

### News/Content
| Site | Status |
|------|--------|
| **BBC News** | ✅ Works |
| **Wikipedia** | ✅ Works |
| **Most blogs** | ✅ Works |

## Detection Methods Encountered

1. **CDN-Level (Hard Block)**
   - CloudFront 403
   - Akamai Access Denied
   - Occurs before HTML loads
   - **No workaround**

2. **JavaScript Challenge (Medium)**
   - "Press & Hold"
   - "I'm not a robot"
   - Cookie/session validation
   - **May use text extraction services**

3. **Rate Limiting (Soft)**
   - 429 Too Many Requests
   - Temporary IP blocks
   - **May work with delays**

## Workarounds Attempted (Effectiveness)

- ❌ Different user agents
- ❌ Session building with cookies
- ❌ Mobile user agents
- ❌ Referrer headers
- ⚠️ Text extraction services (r.jina.ai) - Mixed results
- ✅ Python requests + BeautifulSoup - Only for unprotected sites

## Recommended Approach

1. **Try browser navigation first**
2. **If blocked, check alternatives** (similar data, less protection)
3. **For critical data, ask user to paste** (manual extraction)
4. **Never attempt circumvention** of ToS-protected sites

## Signs of Bot Detection

```
- "Your request could not be processed"
- Reference IDs in error messages
- "Press & Hold to confirm you're human"
- 403 CloudFront errors
- Empty page loads
- "Are you a robot?" pages
```

---

Created from experience with real estate scraping task
