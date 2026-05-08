---
name: google-warranty
description: Google Pixel device warranty & repair request flow. Pixel phones, Pixel Watch, Pixel Buds.
version: 1.0.0
parent: find-warranty-and-repair-pages
metadata:
  manufacturer: Google
  products: [Pixel phone, Pixel Watch, Pixel Buds, Pixel Fold]
  portal_url: https://support.google.com/pixelphone/
---

# Google Pixel Warranty & Repair

## Quick Reference

| Resource | URL |
|----------|-----|
| **Pixel support home** | `https://support.google.com/pixelphone/` |
| **Repair & Warranty Learning Center** | Via "Get started with Pixel Repairs" link |
| **Warranty check** | Settings → About Phone → Warranty on device, or via support |
| **Authorized repair** | uBreakIFix (Google's authorized repair partner) |
| **Google Store repairs** | `https://store.google.com/us/product/` |

## Repair Flow

### Step 1: Go to Pixel support

```
https://support.google.com/pixelphone/
```

### Step 2: Navigate to repairs

1. Click **"Get started with Pixel Repairs"** in the top nav
2. This opens the **Repair & Warranty Learning Center**
3. From there: **Initiate a repair** → **Find the best repair option for you**

### Step 3: Choose repair option

Google offers **three repair options**:

1. **Walk-in repair** — Take device to a uBreakIFix store
2. **Mail-in repair** — Ship device to Google/partner repair center
3. **DIY with Repair mode** — Use Repair mode to self-repair (Pixel 6+)

## Repair Options

### Option 1: Walk-in Repair (uBreakIFix)

- **Find a location**: `https://support.google.com/pixelphone/repair` (via "Find an authorized repair partner" link)
- uBreakIFix is Google's authorized repair partner
- Uses genuine Google parts
- Covered by Google's warranty

### Option 2: Mail-in Repair

1. Initiate repair via Pixel support
2. Google sends a repair kit with packaging
3. Ship device to repair center
4. Receive repaired/replacement device
5. Typical turnaround: 7–10 business days

### Option 3: Repair Mode (DIY, Pixel 6+)

**Repair mode** is a feature that lets you self-repair:
- Protects your data during repair
- Enable via Settings → Repair mode
- After repair, exit repair mode to restore full access

## Pixel Repair & Warranty Learning Center Sections

The Learning Center (accessible via "Get started with Pixel Repairs") has 5 sections:

1. **Check warranty eligibility**
   - Confirm warranty coverage
   - What affects warranty eligibility
   - In-warranty vs out-of-warranty

2. **Initiate a repair**
   - Find the best repair option for you
   - Get ready to start a repair
   - Find an authorized repair partner
   - Walk-in repair
   - Mail-in repair

3. **Use Repair mode**
   - How Repair mode works
   - Access Repair mode
   - Exit Repair mode

4. **Get repair status updates**
   - Track mail-in repair
   - Find shipping status
   - Check walk-in repair
   - Order/Repair history

5. **Understand repair charges**
   - Authorizations & charges
   - Estimated repair cost
   - In-warranty repairs

## Common Pixel Issues

| Issue | Route |
|-------|-------|
| Cracked screen | Walk-in (uBreakIFix) or mail-in |
| Battery replacement | Walk-in or mail-in |
| Charging port | Walk-in or mail-in |
| Camera issues | Walk-in or mail-in |
| Water damage | Assessment at uBreakIFix |
| Screen flicker/display | Mail-in or walk-in |

## Google Pixel Warranty Terms

| Product | Warranty |
|---------|----------|
| Pixel phone | 1 year from purchase |
| Pixel Watch | 1 year from purchase |
| Pixel Buds | 1 year from purchase |
| Pixel Fold | 1 year from purchase |

**Warranty covers:** Manufacturing defects, hardware failures under normal use.

**Warranty does NOT cover:**
- Physical damage (cracks, dents)
- Liquid damage (unless Pixel is water-resistant and damage is not due to misuse)
- Unauthorized modifications
- Normal wear and tear

## Repair Costs (Out-of-Warranty, Approximate)

| Repair | Cost (approx.) |
|--------|----------------|
| Pixel 8 Pro screen | $180–$220 |
| Pixel 8 Pro battery | $80–$100 |
| Pixel 7 screen | $130–$170 |
| Pixel 7 battery | $70–$90 |
| Pixel Watch screen | $140–$180 |
| Pixel Buds battery | $50–$70 |

Actual cost depends on model and repair provider.

## Serial Number Locations

| Device | Location |
|--------|----------|
| Pixel phone | Settings → About phone → IMEI / Serial number |
| Pixel Watch | Settings → About → Serial number |
| Pixel Buds | Inside case or Settings → Bluetooth → Pixel Buds |
| Original packaging | Barcode label on box |

## Automation Notes

### What we found:
- ✅ **Google support is accessible** — No bot detection blocking the Pixel support site
- ✅ **Standard HTML** — Clean support articles and navigation
- ⚠️ **Repair initiation requires sign-in** — "Contact us" or repair request flow requires Google account
- ⚠️ **Repair Learning Center uses SPA navigation** — article URLs may change; use nav links
- ✅ **Repair mode feature** (Pixel 6+) — enables DIY repair without data security concerns

### Automation approach:
- **Warranty info**: Guide user to Settings → About Phone on their device
- **Repair options**: Open Pixel support and navigate to Repair & Warranty Learning Center
- **Repair request**: Manual mode recommended — requires Google account sign-in

## References

- Pixel Phone Help: `https://support.google.com/pixelphone/`
- Repair & Warranty Learning Center: Via "Get started with Pixel Repairs" link
- uBreakIFix: Find via Pixel support or `https://www.ubreakifix.com/`
- Google Store: `https://store.google.com/`
