---
name: apple-warranty
description: Apple device warranty & repair request flow. iPhone, Mac, iPad, Apple Watch, AirPods, Vision Pro.
version: 1.0.0
parent: find-warranty-and-repair-pages
metadata:
  manufacturer: Apple
  products: [iPhone, iPad, Mac, Apple Watch, AirPods, Vision Pro]
  portal_url: https://support.apple.com/repair
  support_url: https://support.apple.com
---

# Apple Warranty & Repair

## Quick Reference

| Resource | URL |
|----------|-----|
| **Repair hub** | `https://support.apple.com/repair` |
| **iPhone repair** | `https://support.apple.com/iphone/repair` |
| **Mac repair** | `https://support.apple.com/mac/repair` |
| **iPad repair** | `https://support.apple.com/ipad/repair` |
| **Apple Watch repair** | `https://support.apple.com/watch/repair` |
| **AirPods repair** | `https://support.apple.com/airpods/repair` |
| **Coverage check** | `https://checkcoverage.apple.com/` |
| **My Support** | `https://supportprofile.apple.com/` |

## Repair Flow

**Two entry points:**

1. **Guided flow** — `https://support.apple.com/repair` → select device → select topic → repair options
2. **Direct repair page** — `https://support.apple.com/{product}/repair` → select model → get service

Both lead to the same repair options: **Make a Reservation** (Genius Bar) or **Send in for Repair** (mail-in).

### Entry Point A: Guided Flow

**URL**: `https://support.apple.com/repair`

1. Page shows device grid: iPhone, Mac laptops, iPad, Apple Watch, AirPods, More
2. Click your device
3. Select topic category:
   - **Repairs & Physical Damage** — cracked screen, battery, water damage, etc.
   - Device Performance — slow, freezing, crashes
   - Subscriptions & Purchases
   - Apple Store Shopping
   - Passwords & Security
   - Update, Backup & Restore
   - More
4. Select specific issue from radio buttons (e.g., "Unable to power on", "Cracked screen")
5. Click **Continue**
6. Page shows: Solutions + **Repair Options** (Make a Reservation / Send in for Repair)
7. Click **Get started** under the desired repair option

### Entry Point B: Direct Repair Page

**URL**: `https://support.apple.com/iphone/repair` (or `/mac/repair`, etc.)

1. Select your **Device Type** from dropdown
2. Select your **Model** from second dropdown
3. Click **Get service**
4. Proceed to repair options

## Repair Options

### Option 1: Make a Reservation (Genius Bar)

- In-person service at an Apple Store
- Requires Apple ID sign-in
- Bring the device + proof of purchase
- Walk-in may be available but reservation recommended
- **URL for store locator**: `https://locate.apple.com/`

### Option 2: Send in for Repair (Mail-In)

- Ships device to Apple repair center
- Free standard shipping both ways
- Apple sends packaging kit via email
- Typical turnaround: 7–10 business days
- Requires Apple ID sign-in

### Option 3: Apple Authorized Service Provider

- Third-party shops authorized by Apple
- Uses genuine Apple parts
- Covered by Apple warranty
- Find at: `https://support.apple.com/repair/reseller`

## iPhone Issue Categories (Repairs & Physical Damage)

| Topic | Description |
|-------|-------------|
| Cracked screen (front only) | Front glass only |
| Battery service | Battery replacement |
| Back of iPhone is damaged | Rear glass |
| Both front and back damaged | Full device damage |
| Screen or display quality | Display defects (no physical damage) |
| **Unable to power on** | Device not turning on |
| Camera not working as expected | Camera issues |
| Liquid or water damage | Water exposure |
| Sound or speakers | Audio problems |
| Cables, headphones, and adapters | Accessory issues |

## Common Issues by Product

### iPhone

- **Screen repair**: Apple's Screen Replacement program — out-of-warranty fee applies
- **Battery**: In-warranty = free; out-of-warranty = $69–$129 depending on model
- **Water damage**: Not typically covered under standard warranty — AppleCare+ may cover
- **Serial number**: Settings → General → About → IMEI, or Settings → General → About → Serial Number

### Mac

- **Battery service**: In-warranty = free; out-of-warranty = $129–$199
- **Keyboard/Trackpad**: Covered under Apple Keyboard Service Program if eligible
- **Logic board**: Major repair — check AppleCare+ status first
- **Serial number**: Apple menu → About This Mac → Serial Number

### iPad

- **Screen**: Apple Pencil + touch issues; battery replacement
- **Smart Keyboard**: Connection issues
- **Serial number**: Settings → General → About → Serial Number

### Apple Watch

- **Battery**: Built-in, not user-replaceable
- **Screen/crack**: Apple Watch repair or replacement
- **Band issues**: Not covered under warranty
- **Serial number**: Settings → General → About → Serial Number

### AirPods

- **Battery**: rechargeable battery has limited lifespan; out-of-warranty replacement available
- **One earbud not working**: Try resetting (Settings → Bluetooth → AirPods → forget → reconnect)
- **Serial number**: Inside the AirPods case lid, or original packaging

## Apple Repair Form Fields

When starting a mail-in repair:

| Field | Notes |
|-------|-------|
| Apple ID | Sign-in required |
| Device serial number | Must be entered — auto-detected if signed in |
| Problem description | Dropdown or free text depending on issue |
| Purchase date | For warranty validity check |
| Proof of purchase | Photo upload optional |

## Automation Notes

**This skill has been tested — Apple repair flow is highly automation-friendly.**

### What works:
- ✅ Clean HTML (no shadow DOM, no Oracle APEX)
- ✅ Standard radio buttons and links — `browser_click` works reliably
- ✅ Direct URL pattern: `support.apple.com/{product}/repair`
- ✅ Dropdown comboboxes for device/model selection — `browser_click` on options works
- ✅ AJAX navigation — clicking updates content without full page reload
- ✅ No anti-bot protection detected

### Navigation patterns:
- `browser_click` on radio buttons selects them cleanly
- "Continue" button enables after selecting a radio option
- "Get service" link advances to repair options
- Some links (inside listitems) may require clicking the heading, not just the listitem

### Two main URL patterns:
```
https://support.apple.com/repair                          # hub — select device
https://support.apple.com/{product}/repair               # direct repair page
https://getsupport.apple.com/solutions                   # AJAX-powered guided flow
```

## Out-of-Warranty Repair Pricing (US, 2026)

| Repair | Out-of-Warranty | AppleCare+ |
|--------|-----------------|------------|
| iPhone screen (iPhone 16/17) | $229 | $29 |
| iPhone screen (older) | $169–$199 | $29 |
| iPhone battery | $89–$129 | $0 |
| MacBook Pro 14" screen | $399 | $99 |
| MacBook Air screen | $299 | $99 |
| MacBook battery | $129–$199 | $0 |
| MacBook keyboard | $129–$299 | $0 (if eligible) |
| iPad Pro 13" screen | $399 | $49 |
| iPad Air screen | $229 | $29 |
| iPad battery | $99 | $0 |
| Apple Watch Series 10 battery | $79 | $0 |
| Apple Watch Ultra battery | $79 | $0 |
| AirPods Pro battery | $89/earbud | N/A |
| AirPods battery (non-Pro) | $69/earbud | N/A |

*Prices are approximate and vary by model. Contact Apple for a quote.*

---

## Pricing Reference (US, 2026)

| Repair | In-Warranty | Out-of-Warranty | AppleCare+ |
|--------|-------------|-----------------|------------|
| iPhone screen (iPhone 17) | Free | $229 | $29 |
| iPhone battery | Free | $89–$129 | $0 |
| MacBook screen | Free | $299–$599 | $99 |
| Mac battery | Free | $129–$199 | $0 |
| iPad screen | Free | $229–$399 | $29–$49 |
| Apple Watch battery | Free | $79 | $0 |
| AirPods battery | N/A | $89/earbud | N/A |

## Auto-Fill vs. Manual

Apple repair forms require **Apple ID sign-in** — the form fields are pre-filled from the user's account.

**Ask**: *"Apple repair requires signing in. Would you like me to open the repair page so you can sign in and fill it yourself?"*

Auto-fill is limited for Apple because:
1. Apple ID authentication is required
2. Form fields are tied to the signed-in account
3. Serial number and device info are pre-populated from the account

**Best approach**: Open the repair URL for the user, let them sign in and complete the form.

## Serial Number Locations

| Device | Location |
|--------|----------|
| iPhone | Settings → General → About → Serial Number / IMEI |
| iPad | Settings → General → About → Serial Number |
| Mac | Apple menu → About This Mac → Serial Number |
| Apple Watch | Settings → General → About → Serial Number |
| AirPods | Inside case lid, or Settings → Bluetooth → AirPods → info |
| Vision Pro | Settings → General → About → Serial Number |

## References

- Repair hub: `https://support.apple.com/repair`
- Coverage check: `https://checkcoverage.apple.com/`
- Apple Store reservations: `https://locate.apple.com/`
- Apple Authorized Service Providers: `https://support.apple.com/repair/reseller`
- AppleCare products: `https://www.apple.com/support/products/`
