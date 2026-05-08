---
name: find-returns
description: "Navigate retailer return/exchange portals — initiate returns, print labels, track refunds, manage 30-day windows. Umbrella: Amazon, Zara, H&M, clothing."
version: 1.0.0
category: research
metadata:
  type: umbrella
  retail_categories: [electronics, apparel, home, marketplace]
  standard_return_window: 30 days
  sub_skills: [amazon-returns, zara-returns, hm-returns, clothing-returns]
---

# Find Returns — Return & Exchange Portal Skill

## Overview

This is an **umbrella skill** for initiating product returns and exchanges across major retailers. Each sub-skill covers retailer-specific return policies, portals, and automatable steps.

## Architecture

```
find-returns/                      ← umbrella (you are here)
├── amazon-returns/               ← marketplace sub-skill
├── zara-returns/                  ← apparel sub-skill
├── hm-returns/                    ← apparel sub-skill
└── clothing-returns/              ← general apparel sub-skill
```

## Standard Return Workflow

Most retailers follow this pattern:

### Step 1: Check Return Window
- **Standard**: 30 days from delivery
- **Clothing**: Some extend to 60–90 days (Zara: 30 days, H&M: 30 days with receipt)
- **Marketplace**: Amazon allows 30 days for most items; some categories vary
- **Electronics**: Usually 15–30 days (Apple: 15 days, Best Buy: 15 days)

### Step 2: Locate Order
- Sign into account on retailer website
- Find order history or "Returns & Orders"
- Locate the specific item to return

### Step 3: Initiate Return
- Select return reason (wrong item, defective, changed mind, etc.)
- Choose refund method (original payment, store credit, exchange)
- Select return shipping method (prepaid label vs. drop off)

### Step 4: Ship or Drop Off
- Print prepaid return label (email or account)
- Pack item securely with all original packaging/tags
- Ship via carrier or drop at designated location

### Step 5: Track Refund
- Most refunds process within 5–10 business days after delivery
- Credit card refunds may take 1–2 billing cycles
- Store credit typically immediate

## Return Reason Codes (Standard)

| Reason | Description | Notes |
|--------|-------------|-------|
| Wrong item received | Item doesn't match order | Free return shipping |
| Defective/Damaged | Product arrived broken or doesn't work | Free return shipping |
| Changed mind | No longer want the item | May have return shipping fee |
| Better price found | Price dropped after purchase | Varies by retailer |
| Doesn't fit | Clothing doesn't fit | Free for some retailers |
| Not as described | Item differs from listing | Free return shipping |
| Arrived too late | Missed deadline or no longer needed | Varies |

## Refund Methods

| Method | Processing Time | Notes |
|--------|----------------|-------|
| Original payment | 5–10 business days | Standard for most retailers |
| Store credit | Immediate | Often fastest option |
| Exchange | Varies | Replacement ships after return received |
| Gift card | Immediate | Available at most retailers |

## Common Pitfalls

- **Return window expired**: Some retailers have strict cutoffs — check early
- **Original packaging required**: Missing box/packaging may result in restocking fee
- **Final sale items**: Electronics, intimates, earrings usually non-returnable
- **Marketplace sellers**: Third-party Amazon sellers have their own policies
- **Clothing tags removed**: Must have original tags attached
- **Fashion retailer WAF**: Zara, H&M, ASOS, Urban Outfitters, and most EU-origin fashion brands use PerimeterX/bot protection that blocks all headless browser automation. Returns for these retailers are **manual-only** — guide the user step by step. Do not attempt automation.

## What Makes Returns Hard to Automate

| Blocker | Example |
|---------|---------|
| CAPTCHA on return portal | Amazon sometimes shows CAPTCHA |
| Account sign-in required | Must be logged in to access orders |
| Order ID in URL or session | Order-specific tokens prevent direct URL access |
| Anti-bot protection | Heavy JS rendering on some retailer sites |
| Multi-step form with state | Return reason → shipping method → label download |
| Drop-off only for large items | Furniture, appliances can't be shipped |

## How to Use This Skill

1. **Identify the retailer** — "amazon", "zara", "hm", or "other"
2. **Load the sub-skill** — e.g. `skill_view(name='amazon-returns')`
3. **Follow the retailer's specific flow** — steps differ per retailer
4. **Choose auto-fill or manual** — auto-fill where automation works, manual fallback

## Sub-Skills

| Retailer | Category | Automatable | URL Pattern |
|----------|----------|-------------|-------------|
| amazon-returns | Marketplace | ⚠️ Partial | amazon.com/returns |
| zara-returns | Apparel | ⚠️ Partial | zara.com → account |
| hm-returns | Apparel | ⚠️ Partial | hm.com → account |
| clothing-returns | Apparel | ⚠️ Partial | Varies by retailer |

## Quick Reference: Return Windows

| Retailer | Return Window | Notes |
|----------|--------------|-------|
| Amazon | 30 days | Most items; some categories differ |
| Zara | 30 days | Must have receipt; online purchases to store or mail |
| H&M | 30 days | With receipt; online purchases to store or mail |
| Apple | 15 days | Must have receipt |
| Best Buy | 15 days | Most items; extended holidays |
| Target | 30 days | General; some electronics 15 days |
| Walmart | 90 days | With receipt |
| Nordstrom | None | Always free returns |

## References

See `references/return-portals.md` for the full directory of return portal URLs across all supported retailers.
