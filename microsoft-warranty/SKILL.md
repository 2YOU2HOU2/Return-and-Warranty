---
name: microsoft-warranty
description: Microsoft device warranty & repair request flow. Xbox consoles, Surface tablets, Windows PCs.
version: 1.0.0
parent: find-warranty-and-repair-pages
metadata:
  manufacturer: Microsoft
  products: [Xbox, Surface, Windows PC]
  portal_url: https://support.xbox.com/
---

# Microsoft Warranty & Repair

## Quick Reference

| Resource | URL |
|----------|-----|
| **Xbox Support** | `https://support.xbox.com/` |
| **Surface Support** | `https://support.microsoft.com/en-us/surface` |
| **Surface repair article** | `https://support.microsoft.com/en-us/surface/how-to-get-service-or-repair-for-surface-749e4a85-1e3c-4de6-a862-ff66f55ce994` |
| **Device management** | `https://account.microsoft.com/devices` |
| **Xbox warranty info** | Search: "Xbox console warranty" on support.xbox.com |

## Repair Flow

### Xbox

**URL**: `https://support.xbox.com/`

**Known limitation**: Direct repair URLs on Xbox support site return 404 or "page not found". The actual repair flow requires **Microsoft Account sign-in**.

#### Xbox Repair Path:

1. Go to `https://support.xbox.com/`
2. Sign in with Microsoft Account
3. Navigate to: Account → Devices → Select console → Start repair
4. Or use: `https://account.microsoft.com/devices`
5. Select device → "Start repair" → follow prompts

**Xbox warranty**: 1-year manufacturer warranty from purchase date. Replacement components have 90-day warranty.

#### Xbox Repair Options:

1. **Online repair request** — via account.microsoft.com/devices (sign-in required)
2. **Xbox authorized service provider** — find at Xbox support
3. **Microsoft Store** — in-person service at select Microsoft Store locations

### Surface

**URL**: `https://support.microsoft.com/en-us/surface`

#### Surface Repair Path:

1. Go to Surface support page
2. Click **"Get service"** or find the repair article
3. Sign in with Microsoft Account
4. Select Surface model
5. Describe the issue
6. Choose service option: **Mail-in repair** / **Find a local repair shop** / **Surface product replacement**

#### Surface Service Options:

| Option | Description |
|--------|-------------|
| Mail-in repair | Ship to Microsoft repair center |
| In-person | Find a local Microsoft Authorized Service Provider |
| Advanced Exchange | Get replacement first (fee + deposit), then return broken device |

## Common Surface Issues

| Issue | Route |
|-------|-------|
| Screen cracked | Screen repair/replacement |
| Keyboard not working | Type Cover issues |
| Battery drain | Battery service |
| Won't turn on | Power issues |
| Touchpad issues | Hardware service |

## Microsoft Repair Form Fields

| Field | Notes |
|-------|-------|
| Microsoft Account | Sign-in required |
| Device serial number | Found in Settings → System → About |
| Device model | Pre-filled from account if registered |
| Problem description | Dropdown or free text |
| Proof of purchase | For warranty validation |

## Serial Number Locations

| Device | Location |
|--------|----------|
| Xbox console | Settings → System → Console info → Serial number |
| Surface | Settings → System → About → Serial number |
| Windows PC | `wmic bios get serialnumber` or Settings → System → About |

## Automation Notes

### What we found:
- ⚠️ **Sign-in required** — Both Xbox and Surface repair flows require Microsoft Account authentication.
- ⚠️ **Broken direct URLs** — Many `support.xbox.com` repair URLs return 404. Site structure appears to have changed.
- ⚠️ **Account page timeout** — `account.microsoft.com/devices` requires active session — cannot access without sign-in.
- ✅ **Standard HTML** — Once authenticated, the repair form uses standard HTML elements.

### Automation approach:

**For users with Microsoft Account:**
1. Navigate to `https://account.microsoft.com/devices`
2. Sign in with `browser_type` on email/password fields
3. Select device → Start repair
4. Fill repair request form with standard `browser_click` / `browser_type`

**For users without Microsoft Account:**
Manual mode — direct user to open the page and sign in themselves.

### Xbox-specific notes:
- Xbox warranty is **1 year** for the console, **90 days** for replacement components
- For out-of-warranty repairs, Microsoft will quote a price before proceeding
- Extended warranty (Xbox All Access) may include coverage

## Warranty Information

| Product | Warranty |
|---------|----------|
| Xbox console | 1 year from purchase |
| Xbox replacement parts | 90 days |
| Surface | 1 year limited hardware warranty |
| Surface + Keyboard | Covered under Surface warranty |
| Microsoft Complete (extended) | Up to 3 years |

## Out-of-Warranty Repair Pricing (US, 2026)

| Repair | Out-of-Warranty (est.) |
|--------|----------------------|
| Xbox Series X HDMI port | $150–$250 |
| Xbox Series S HDMI port | $120–$200 |
| Xbox One HDMI port | $80–$150 |
| Xbox controller drift | $30–$50 |
| Surface Pro 10 screen | $300–$400 |
| Surface Pro 10 keyboard | $100–$150 |
| Surface Pro battery | $150–$200 |
| Surface Laptop Studio screen | $250–$350 |

*Prices are estimates through Microsoft or authorized repair. Contact Microsoft for a quote. Microsoft Complete owners may have reduced costs.*

## References

- Xbox Support: `https://support.xbox.com/`
- Surface Support: `https://support.microsoft.com/en-us/surface`
- Device Management: `https://account.microsoft.com/devices`
- Surface Repair Article: `https://support.microsoft.com/en-us/surface/how-to-get-service-or-repair-for-surface-749e4a85-1e3c-4de6-a862-ff66f55ce994`
