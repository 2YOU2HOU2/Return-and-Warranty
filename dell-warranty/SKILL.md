---
name: dell-warranty
description: Dell device warranty & repair request flow. XPS, Inspiron, Latitude, Alienware, OptiPlex.
version: 1.0.0
parent: find-warranty-and-repair-pages
metadata:
  manufacturer: Dell
  products: [XPS laptop, Inspiron, Latitude, Alienware, OptiPlex, Dell monitor]
  portal_url: https://www.dell.com/support/
  warning: Heavy bot detection — most support pages return Access Denied
---

# Dell Warranty & Repair

## Quick Reference

| Resource | URL | Notes |
|----------|-----|-------|
| **Support home** | `https://www.dell.com/support/` | BLOCKED by bot detection |
| **Service tag lookup** | `https://www.dell.com/en-us/servicetag/` | BLOCKED |
| **Warranty check** | `https://www.dell.com/support/warranty` | BLOCKED |
| **Repair scheduling** | `https://www.dell.com/support/repair/` | BLOCKED |

## ⚠️ Critical Warning: Bot Detection

**Dell.com has extremely aggressive bot detection.** The Browserbase headless session cannot access:
- `dell.com/support/*` — returns "Access Denied"
- `dell.com/en-us/servicetag/` — returns "Access Denied"
- SOAP API (`api.dell.com`) — returns "Policy Falsified"

**Options to work around:**
1. Use **residential proxies** (Browserbase Scale plan with advanced stealth)
2. Use **real Chrome + CDP** method (like we did for Sony) in a separate session
3. **Manual mode** — direct user to visit dell.com themselves

## Repair Flow (Manual Mode)

If bot detection cannot be bypassed, guide the user manually:

### Step 1: Find your Service Tag

The Service Tag is a 7-character alphanumeric code on your Dell device:
- **Laptops**: Bottom panel, near serial number
- **Desktops**: Back panel
- **Monitors**: Back label

### Step 2: Check warranty status

1. Go to `https://www.dell.com/en-us/servicetag/`
2. Enter your Service Tag
3. View warranty status and expiration

### Step 3: Start repair

**If in warranty:**
1. Sign in at `https://www.dell.com/support/`
2. Select device from your account
3. Click "Start a repair" or "Contact support"
4. Choose: On-site / Mail-in / In-person

**If out of warranty:**
1. Sign in at `https://www.dell.com/support/`
2. Select device
3. Click "Out of Warranty repair" — Dell will quote a price

## Dell Warranty Terms

| Product | Warranty |
|---------|----------|
| XPS, Inspiron, Latitude | 1 year basic hardware |
| Alienware | 1 year basic + Alienware Premium Support |
| OptiPlex | 1 year basic |
| Dell monitors | 1 year advanced exchange |
| Extended warranty | Available via Dell Protection Plans |

## Dell Repair Options

| Option | Description | Warranty | Out-of-Warranty |
|--------|-------------|----------|-----------------|
| On-site Repair | Technician visits your location | Covered | Fee applies |
| Mail-in Repair | Ship to Dell repair center | Covered | Fee applies |
| In-person | Bring to Dell storefront | Covered | Fee applies |

## Dell Service Center Locator

URL: `https://www.dell.com/support/incidents/us/en/inc locator/14`

## Dell Support API

Dell has a SOAP API at `api.dell.com/support/v2/assetinfo/warranty` but it requires valid policy tokens. Not accessible without proper authentication.

## Serial Number / Service Tag Locations

| Device | Location |
|--------|----------|
| Laptop | Bottom panel (white label) |
| Desktop | Back panel |
| Monitor | Back label |
| BIOS | Press F2 at boot → Serial number info |

## Dell Repair Form Fields

| Field | Notes |
|-------|-------|
| Service Tag | 7-character code (e.g., "ABC1234") |
| Product serial number | Full serial number |
| Express Service Code | Numeric version of Service Tag |
| Error code | For diagnostic submission |
| Dell account | Sign-in required for repair initiation |

## Automation Notes

### What we found:
- 🔴 **Severe bot detection** — All main support pages return "Access Denied"
- 🔴 **No residential proxy** — Browserbase session is blocked
- ⚠️ **SOAP API blocked** — `api.dell.com` returns Policy Falsified
- ✅ **Community forum accessible** — `dell.com/community/` works

### Automation approach:
**Best option: Real Chrome + CDP**
1. In a separate terminal, launch Chrome with remote debugging: `open -a "Google Chrome" --args --remote-debugging-port=9222 --user-data-dir="..."`
2. Connect Playwright via CDP to the real Chrome session
3. Navigate to dell.com — real browser passes bot detection
4. Continue with repair flow

**If CDP is not available: Manual mode only**

## Out-of-Warranty Repair Pricing (US, 2026)

| Repair | Out-of-Warranty (est.) |
|--------|----------------------|
| XPS 13 screen | $250–$350 |
| XPS 15 screen | $300–$400 |
| XPS 13 battery | $100–$150 |
| Latitude battery | $80–$130 |
| Alienware laptop screen | $200–$350 |
| Dell monitor screen | $100–$200 |
| Inspiron laptop keyboard | $60–$100 |
| Dell power adapter | $40–$80 |

*Dell typically quotes exact prices through their repair center. Out-of-warranty repair through Dell can be expensive — third-party repair shops often 40–60% cheaper for common issues.*

## References

- Support home: `https://www.dell.com/support/` (blocked)
- Service tag lookup: `https://www.dell.com/en-us/servicetag/` (blocked)
- Warranty check: `https://www.dell.com/support/warranty` (blocked)
- Community (accessible): `https://dell.com/community/`
