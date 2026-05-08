---
name: nintendo-warranty
description: Nintendo device warranty & repair request flow. Nintendo Switch, Joy-Con, game cards.
version: 1.0.0
parent: find-warranty-and-repair-pages
metadata:
  manufacturer: Nintendo
  products: [Nintendo Switch, Joy-Con, Switch Lite, Switch OLED, game cards]
  portal_url: https://www.nintendo.com/us/switch/
---

# Nintendo Warranty & Repair

## Quick Reference

| Resource | URL |
|----------|-----|
| **Nintendo Switch home** | `https://www.nintendo.com/us/switch/` |
| **Switch support** | `https://www.nintendo.com/us/switch/support/` (may require JS navigation) |
| **Service Center** | Via support page or Nintendo's repair partner |
| **Warranty info** | `https://www.nintendo.com/us/switch/warranty/` |
| **Joy-Con drift repair** | Through Nintendo Service Center or store |

## Repair Flow

### Step 1: Find repair options

Navigate to Nintendo support via the main site:
1. Go to `https://www.nintendo.com/us/switch/`
2. Click **Support** tab (top navigation)
3. Select **Nintendo Switch** from the support menu
4. Look for **"Service Center"** or **"Repairs"** link

**Note**: Nintendo's site uses heavy JavaScript — direct URL navigation to `/support/` and `/service-center/` paths may return 404. Use the top navigation to find support links.

### Step 2: Identify the repair path

Nintendo offers several repair options:

1. **Nintendo Service Center** — Mail-in repair via Nintendo's authorized repair partner
2. **Retailer return** — For defective products within return window
3. **Game card issues** — Usually not repaired; replacement of game card if defective

### Step 3: Nintendo Switch Joy-Con Drift

Joy-Con stick drift is a common issue:
- **In warranty**: Nintendo will repair/replace free of charge
- **Out of warranty**: Nintendo may offer a reduced-cost repair or replacement
- **Steps**: Contact Nintendo support → request repair → ship Joy-Con → receive repaired/new unit

## Nintendo Warranty Terms

| Product | Warranty |
|---------|----------|
| Nintendo Switch console | 1 year from purchase |
| Joy-Con controllers | 1 year from purchase |
| Game cards | 90 days from purchase |
| Nintendo Switch Lite | 1 year from purchase |

**Warranty does NOT cover:**
- Physical damage (drops, spills, etc.)
- Modifications or unauthorized repairs
- Normal wear and tear (except Joy-Con drift in some regions)

## Nintendo Repair Form Fields

| Field | Notes |
|-------|-------|
| Product | Nintendo Switch, Joy-Con, etc. |
| Serial number | Required for warranty validation |
| Problem description | Free text |
| Purchase date | For warranty validity |
| Proof of purchase | Receipt or invoice |

## Serial Number Locations

| Device | Location |
|--------|----------|
| Nintendo Switch | Settings → Console → Serial Number |
| Joy-Con | Not independently serialized — pair with console |
| Switch Lite | Settings → Console → Serial Number |
| Game card | Not serialized |

## Automation Notes

### What we found:
- ⚠️ **JavaScript-heavy site** — Direct URLs to support/service pages often return 404. Navigation must go through the top nav menu.
- ⚠️ **No direct repair form URL** — The repair request form has no discoverable public URL; requires navigating through the support flow.
- ⚠️ **Session/state may be required** — Some repair flows may require Nintendo account sign-in.
- ✅ **Standard HTML elements** — Once on the correct page, form elements use standard HTML.

### Automation approach:
1. Navigate through top nav: Support tab → Nintendo Switch → look for repair/service link
2. If JavaScript navigation fails, fall back to **Manual mode** — direct user to the site
3. Nintendo's repair partner (UPS Stores or authorized centers) may have their own simpler form

### Known Nintendo support URLs (confirmed):
```
https://www.nintendo.com/us/switch/                  # Switch home
https://www.nintendo.com/us/switch/warranty/         # Warranty info (may 404)
https://www.nintendo.com/us/switch/service-center/   # Service center (may 404)
```

## Common Issues

| Issue | Route |
|-------|-------|
| Joy-Con drift | Nintendo Service Center repair/replacement |
| Switch won't turn on | Check power cable, try different outlet; if persists → service center |
| Game card won't read | Try cleaning game card; if persists → replacement or repair |
| Screen damage | Nintendo Service Center — physical damage not covered by warranty |
| Battery drain | In-warranty = free service; out-of-warranty = fee |
| Dock HDMI issues | Try different HDMI cable; if persists → service center |

## Out-of-Warranty Repair Pricing (US, 2026)

| Repair | Out-of-Warranty (est.) |
|--------|----------------------|
| Joy-Con stick drift | $30–$50 (per Joy-Con) |
| Joy-Con battery | $20–$40 |
| Switch Lite screen | $100–$150 |
| Switch OLED screen | $150–$200 |
| Switch Dock HDMI port | $40–$80 |
| Game card reader | $30–$60 |
| Battery replacement (Switch) | $40–$70 |

*Joy-Con drift is a common known issue — Nintendo may offer free repair even out of warranty in some cases. Contact Nintendo support.*

## References

- Nintendo Switch home: `https://www.nintendo.com/us/switch/`
- Support (via navigation): Support tab on main site
- Warranty: `https://www.nintendo.com/us/switch/warranty/`
