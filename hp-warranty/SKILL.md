---
name: hp-warranty
description: HP device warranty & repair request flow. HP printers, laptops, desktops, monitors.
version: 1.0.0
parent: find-warranty-and-repair-pages
metadata:
  manufacturer: HP
  products: [HP printer, HP laptop, HP desktop, HP monitor, HP poly, HP enterprise]
  portal_url: https://support.hp.com/us-en
---

# HP Warranty & Repair

## Quick Reference

| Resource | URL |
|----------|-----|
| **HP Support home** | `https://support.hp.com/us-en` |
| **Warranty check** | `https://support.hp.com/us-en/check-warranty` |
| **Repair center** | `https://support.hp.com/us-en/help/repair` |
| **Contact HP** | `https://support.hp.com/us-en/contact` |
| **Service center locator** | `https://support.hp.com/us-en/service-center` |
| **Sign in** | `https://support.hp.com/wcc-services/s/signin` |

## Repair Flow

### Step 1: Go to HP support

```
https://support.hp.com/us-en
```

### Step 2: Identify your product

HP support uses **serial number / product number** to identify your device.

You can find it:
- On the device label (back/bottom)
- In system BIOS (F2 at boot)
- On the original purchase receipt

### Step 3: Check warranty status

1. Go to `https://support.hp.com/us-en/check-warranty`
2. Enter **serial number** (required)
3. Select **country/region**
4. Click **Check warranty**

### Step 4: Get repair service

**If in warranty:**
1. Go to `https://support.hp.com/us-en/contact`
2. Enter serial number
3. Select **"Contact options"** for your covered device
4. Choose repair option: **Mail-in** / **On-site** / **Find a service provider**

**If out of warranty:**
1. HP will quote a repair price before proceeding
2. Options: HP repair, HP authorized service provider, third-party repair

## HP Repair Options

| Option | Description | Notes |
|--------|-------------|-------|
| Mail-in repair | Ship device to HP | Standard turnaround |
| On-site repair | Technician visits | For select products |
| In-person | HP Authorized Service Provider | Find at service-center page |
| Self repair | HP Sure Key (security) / DIY parts | Limited products |

## Product Categories

| Category | Products |
|----------|----------|
| Printers | DeskJet, Envy, OfficeJet, LaserJet, PageWide |
| Laptops | Spectre, Envy, Pavilion, HP Laptop, EliteBook, ZBook |
| Desktops | ENVY, Pavilion, Slim, Gaming, EliteDesk, Z |
| Monitors | HP Series, Z monitors |
| Poly (audio/video) | Headsets, conference phones, cameras |
| Enterprise | ProLiant servers, networking |

## HP Warranty Terms

| Product | Warranty |
|---------|----------|
| Consumer laptops | 1 year limited |
| Business laptops | 1 year standard (longer with HP Care Pack) |
| Consumer printers | 1 year / up to 3 years with HP+ |
| Business printers | 1 year |
| Monitors | 1 year advanced exchange |
| HP Care Pack | Extended warranty up to 5 years |

## HP Repair Form Fields

| Field | Notes |
|-------|-------|
| Serial number | Required — validated format |
| Product number | Optional alternative |
| Country/region | Required |
| HP account | Optional (recommended for saved products) |

## Serial Number Locations

| Device | Location |
|--------|----------|
| Laptop | Bottom panel label |
| Desktop | Back panel or inside chassis |
| Printer | Back panel or inside front door |
| Monitor | Back label |
| BIOS | F2 at boot → Serial number |

## Automation Notes

### What we found:
- ✅ **Warranty check works without sign-in** — `https://support.hp.com/us-en/check-warranty` is accessible
- ⚠️ **Serial number validation** — format is validated client-side; invalid serials rejected
- ⚠️ **SPA routing** — direct URLs to repair pages may redirect to home page; use navigation through main site
- ⚠️ **Bot detection** — some repair flow routes may be blocked without residential proxies
- ✅ **Standard HTML elements** — once on the correct page, `browser_click` and `browser_type` work

### Automation approach:
1. Navigate to warranty check page directly: `https://support.hp.com/us-en/check-warranty`
2. Use `browser_type` to enter serial number
3. Use `browser_click` to submit
4. Read warranty status from results
5. For repair: navigate through the support flow — may require sign-in

## HP Care Pack (Extended Warranty)

HP Care Pack extends warranty and often includes:
- Priority phone support
- On-site repair
- Reduced turnaround time

Purchase at: `https://www.hp.com/us/en/solutions/carepack.html`

## References

- HP Support: `https://support.hp.com/us-en`
- Warranty check: `https://support.hp.com/us-en/check-warranty`
- Repair center: `https://support.hp.com/us-en/help/repair`
- Service center: `https://support.hp.com/us-en/service-center`
- HP Care Pack: `https://www.hp.com/us/en/solutions/carepack.html`
