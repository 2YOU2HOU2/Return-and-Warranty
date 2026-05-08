---
name: lg-warranty
description: LG device warranty & repair request flow. LG phones (no longer sold in US), LG appliances (fridge, washer, TV), LG audio.
version: 1.0.0
parent: find-warranty-and-repair-pages
metadata:
  manufacturer: LG
  products: [LG phone, LG refrigerator, LG washer, LG dryer, LG TV, LG air conditioner, LG audio]
  portal_url: https://www.lg.com/us/support
---

# LG Warranty & Repair

## Quick Reference

| Resource | URL |
|----------|-----|
| **US Support home** | `https://www.lg.com/us/support` |
| **Schedule repair** | `https://www.lg.com/us/support/repair-service/schedule-repair` |
| **Flat-rate repair** | `https://www.lg.com/us/support/repair-service/flat-rate-repair` |
| **Track repair** | `https://www.lg.com/us/support/track-service-status` |
| **Find service center** | `https://www.lg.com/us/support/find-service-center` |
| **Warranty info** | `https://www.lg.com/us/support` (popup modal) |
| **Contact LG** | `https://www.lg.com/us/support/contact` |

## Repair Flow

### Step 1: Go to LG support

```
https://www.lg.com/us/support
```

### Step 2: Identify repair path

LG has **two main repair options**:

1. **Warranty Repair** — Free for manufacturing defects (requires MyLG sign-in)
2. **Flat-Rate Repair** — $369–$399 fixed fee (appliances only, no sign-in required)

### Path A: Warranty Repair (requires MyLG account)

1. Go to `https://www.lg.com/us/support`
2. Click **"Schedule Repair"**
3. Sign in with **MyLG account**
4. Select product category
5. Enter serial number
6. Describe the issue
7. Choose repair option: **Mail-in** / **On-site** / **Walk-in**
8. Schedule appointment

### Path B: Flat-Rate Repair (appliances only, no sign-in)

1. Go to `https://www.lg.com/us/support/repair-service/flat-rate-repair`
2. Select product category: Refrigerator / Washer / Dryer / Range / Dishwasher / AC
3. Enter **serial number** (required)
4. Enter ZIP code
5. Choose date for technician visit
6. Pay flat rate ($369–$399) via credit card
7. Receive packaging instructions

### Path C: Find a Service Center

1. Go to `https://www.lg.com/us/support/find-service-center`
2. Enter ZIP code
3. Select product category (49 categories available)
4. View list of nearby authorized service centers

## Product Categories

| Category | Products |
|----------|----------|
| Refrigerators | French door, side-by-side, top/freezer |
| Washers & Dryers | Front-load, top-load, all-in-one |
| Ranges / Ovens | Electric, gas, induction |
| Dishwashers | Built-in dishwashers |
| Air Conditioners | Window, portable, split AC |
| TVs | OLED, NanoCell, LED, QNED |
| Phones | **LG phones no longer sold in US** — only chat/phone support available |

## LG Appliance Flat-Rate Repair Pricing

| Appliance | Flat Rate |
|-----------|-----------|
| Refrigerator | $399 |
| Washer | $369 |
| Dryer | $369 |
| Range/Oven | $379 |
| Dishwasher | $369 |
| Air Conditioner | $369 |

Includes parts and labor. Does not cover additional damage found during repair.

## Serial Number Locations

| Appliance | Location |
|-----------|----------|
| Refrigerator | Inside refrigerator compartment, on left wall near top |
| Washer/Dryer | Inside door opening, on the front panel near the drum |
| Range/Oven | Inside oven cavity or on back panel |
| Dishwasher | Inside door panel |
| TV | Back panel label |
| LG phone | Settings → About phone → IMEI |

## Automation Notes

### What we found:
- ⚠️ **MyLG sign-in required** for warranty repairs — cannot automate without credentials
- ✅ **Flat-rate repair** works without sign-in — 4-step wizard with serial number entry
- ⚠️ **Custom combobox elements** — product dropdowns are not standard `<select>` elements
- ⚠️ **Modal dialogs** — flat-rate repair uses `<dialog>` HTML elements
- ⚠️ **JavaScript navigation** — many links use `onclick` handlers instead of hrefs
- ⚠️ **Cookie consent banner** — powered by Transcend, may block automation
- ✅ **Clean URL patterns** — direct URLs to repair pages work

### Automation approach:
- **Warranty repair**: Manual mode recommended (requires sign-in)
- **Flat-rate repair**: Can be partially automated — `browser_click` on dialog buttons, `browser_type` for serial/ZIP
- **Track repair**: Requires phone + reference number (CNN/RNN prefix)

## Warranty Information

| Product | Warranty |
|---------|----------|
| Major appliances | 1 year limited |
| TVs | 1 year limited |
| Phone (if applicable) | 1 year limited |
| Parts | 30 days |
| Labor | 30 days |

Standard warranty does not cover: physical damage, misuse, unauthorized modifications.

## References

- LG Support: `https://www.lg.com/us/support`
- Schedule Repair: `https://www.lg.com/us/support/repair-service/schedule-repair`
- Flat-Rate Repair: `https://www.lg.com/us/support/repair-service/flat-rate-repair`
- Track Repair: `https://www.lg.com/us/support/track-service-status`
- Find Service Center: `https://www.lg.com/us/support/find-service-center`
