---
title: Anti-Bot Protection Detection and Ethical Pivot
name: anti-bot-protection-detection-and-ethical-pivot
description: Recognize aggressive anti-bot protection, attempt reasonable workarounds, and pivot to ethical alternatives when appropriate
triggers:
  - 429 or 403 errors with rotating reference IDs
  - JavaScript challenge pages like KPSDK
  - CloudFront or Cloudflare blocked pages
  - Multiple bypass attempts failing consistently
---

# Anti-Bot Protection Detection and Ethical Pivot

## Overview

This skill helps detect when a website has implemented aggressive anti-bot/anti-scraping protection, attempt reasonable workarounds within ethical bounds, and pivot to legitimate alternatives when bypassing is not appropriate or possible.

## Quick Assessment

### Signs of Strong Protection (Pivot Recommended)
- Different reference IDs on each request
- JavaScript challenges (KPSDK, Cloudflare, DataDome)
- 429/403 errors with no CAPTCHA option
- Response times under 100ms for error pages
- Multiple methods (browser + HTTP) both fail

### Signs of Weak Protection (Continue Trying)
- Same error message
- CAPTCHA challenges present
- Slower response times (actual rendering)
- Soft blocks (redirects, not hard blocks)

## Attempted Workarounds

Try these in order (max 5-10 minutes):

1. **Session building** - Hit main site first, capture cookies
2. **User-agent rotation** - Mobile, Firefox, Edge variants  
3. **Request delays** - 2-5 seconds between requests
4. **Alternative endpoints** - GraphQL, JSON APIs
5. **Text extraction services** - r.jina.ai (note: these also get blocked by CloudFront)

## Red Flags: Stop and Pivot

IMMEDIATELY stop and pivot if:
- Status 429/403 with rotating reference IDs
- "KPSDK" or similar challenge scripts in HTML
- CloudFront or Cloudflare error pages with no user challenge
- Both browser automation AND direct HTTP requests blocked

## Ethical Pivot Alternatives

**Official APIs**
- Many real estate sites offer developer APIs
- Requires registration but is legitimate

**Public Data Sources**
- Government open data portals (Chicago Data Portal, etc.)
- No restrictions on access

**Manual Extraction**
- User visits site normally
- Copies raw data, AI formats it
- Fully legitimate access

**Similar Sites**
- Redfin often has less strict protection than Realtor.com
- Zillow Research offers downloadable datasets

**Third-party Services**
- ATTOM Data, CoreLogic (paid but legitimate)
- MLS data providers

## Communication Template

```
The website is aggressively blocking automated access using [PROTECTION]...

I attempted:
1. [Method 1] - Blocked
2. [Method 2] - Blocked
3. [Method 3] - Blocked

This indicates a hard block that would require bypassing security mechanisms.

Instead, I can help you with:
- [Alternative 1]
- [Alternative 2]
- [Alternative 3]

Which approach would you prefer?
```

## Key Learnings from Realtor.com Case

- **Kasada/KPSDK protection** requires JavaScript execution - not bypassable with simple HTTP requests
- **r.jina.ai** and similar services also blocked by CloudFront on protected sites
- **Cookie-based session building** (KP_UIDz) did not help with IP-level blocks
- **Rotate quickly** - if 3+ approaches fail, protection is enterprise-grade
- **Be transparent** - explain WHY, not just "I cannot"

## What NOT to Do (Without Consideration)

Do NOT attempt these without explicit user authorization:
- IP rotation or proxy services to evade blocks (requires proxy service setup)
- CAPTCHA solving services (paid, may violate TOS)
- Exploiting security vulnerabilities

## Browser Stealth Configurations - Use with Caution

**NOTE**: Recent testing shows `playwright-stealth` CAN bypass Cloudflare for some sites.

For legitimate account creation tasks, try `playwright-stealth`:
```python
from playwright_stealth import Stealth
with Stealth().use_sync(sync_playwright()) as p:
    # browser automation that bypasses Cloudflare
```

However:
- Do NOT use for scraping copyrighted/proprietary data
- Do NOT use to evade bans or abuse rate limits
- Review site's Terms of Service before use
- User should authorize this approach explicitly

See skill `cloudflare-bypass-playwright-stealth` for detailed usage.

## Red Flags: Stop and Pivot (Default Guidance)

If standard methods and stealth both fail, pivot to alternatives:
- Status 429/403 with rotating reference IDs (enterprise protection)
- "KPSDK" or similar advanced challenge scripts
- Both browser automation AND direct HTTP requests blocked
- Account creation blocked at IP level

See the Ethical Pivot Alternatives section above.

## Verification

After pivoting:
- Ensure alternative respects site policies
- Provide concrete help with data formatting
- Note this skill for future similar cases
