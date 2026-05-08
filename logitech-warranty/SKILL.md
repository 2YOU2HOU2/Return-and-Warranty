---
name: logitech-warranty
description: Logitech device warranty & repair request flow. Mice, keyboards, headsets, webcams, speakers, gamepads.
version: 1.0.0
parent: find-warranty-and-repair-pages
metadata:
  manufacturer: Logitech
  products: [Mouse, Keyboard, Headset, Webcam, Speaker, Gamepad, Harmony remote, UE speaker]
  portal_url: https://www.logitech.com/en-us/support
---

# Logitech Warranty & Repair

## Quick Reference

| Resource | URL |
|----------|-----|
| **Logitech Support** | `https://www.logitech.com/en-us/support` |
| **Warranty Info** | No direct URL — embedded in product pages |
| **Extend Protection Plan** | Via support page link |
| **Spare Parts** | `https://www.logitech.com/en-us/support/spare-parts` |
| **Register Product** | Via support page |

## Warranty Terms by Product

| Product Category | Warranty Period |
|-----------------|----------------|
| Mice & Keyboards | 3-year limited hardware warranty |
| Personal Video (webcams) | 2-year limited hardware warranty |
| Headsets | 2-year limited hardware warranty |
| Cameras | 2-year limited hardware warranty |
| Speakers | 2-year limited hardware warranty |
| Gamepads | 2-year limited hardware warranty |
| Harmony Remotes | 1-year limited hardware warranty |
| HARMAN brands (JBL, etc.) | 2-year limited warranty |

**Standard warranty covers:** Manufacturing defects, hardware failures under normal use.

**Warranty does NOT cover:**
- Physical damage (drops, liquid damage, broken parts)
- Damage from misuse or unauthorized modifications
- Normal wear and tear
- Accessories (receivers, cables, batteries unless defective)

## Warranty Check

Logitech does **not** have a public online warranty check tool that accepts a serial number. To check warranty status:

1. **Sign in** to your Logitech account at `https://www.logitech.com/en-us/myalogitech`
2. **Register your product** to activate warranty
3. **Contact support** via chat or phone for warranty status

**Alternative**: If you have the original purchase receipt, that serves as your proof of warranty.

### Serial Number Location

| Product | Serial Number Location |
|---------|----------------------|
| Mouse | Inside battery compartment or on bottom |
| Keyboard | On bottom panel |
| Headset | On the headset (usually inside ear cup) |
| Webcam | On the camera base or cable |
| Receiver | On the USB receiver |
| Original packaging | Barcode label on box |

## Repair / RMA Process

**Important:** Logitech does **not** have a public online repair request form like Apple or Sony. Repairs are handled entirely through customer support.

### Step 1: Contact Logitech Support

Go to `https://www.logitech.com/en-us/support` and:
- Click **CHAT** (recommended) or **PHONE** in the "GET ADDITIONAL ASSISTANCE" section
- Or call: 1-800-231-7717 (US)

### Step 2: Describe Your Issue

Explain the problem to the support agent. They will:
1. Verify your warranty status (may ask for proof of purchase)
2. Troubleshoot basic issues (cable connection, driver issues, etc.)
3. If hardware failure confirmed, initiate an RMA

### Step 3: RMA & Shipping

- If approved, Logitech will provide a prepaid shipping label
- Ship the defective product to Logitech
- Logitech will repair or replace the product
- Return shipping is covered for in-warranty repairs

### Step 4: Timeline

| Stage | Typical Duration |
|-------|-----------------|
| Initial support response | Same day (chat/phone) |
| RMA approval | 1–2 business days |
| Product received & processed | 3–5 business days |
| Repair/replacement completed | 5–7 business days |
| Return shipping | 2–3 business days |

**Total estimated time:** 2–3 weeks

## Extend Protection Plan

Logitech offers an optional **Logitech Protection Plan** (extended warranty):
- Extends coverage beyond standard warranty by 1–2 years
- Covers defects and malfunctions
- Purchase through Logitech support or at time of product registration

Contact Logitech support to learn about available protection plans for your product.

## Out-of-Warranty Repair

| Repair Type | Availability |
|-------------|-------------|
| Spare parts (batteries, receivers, cables) | ✅ Available for purchase at `https://www.logitech.com/en-us/support/spare-parts` |
| Paid repair | ⚠️ Contact support for quote — no public pricing |
| Replacement | ⚠️ May be offered at reduced cost through support |

**Note:** Logitech does not publish out-of-warranty repair pricing. Contact support for a quote.

## Common Issues & Troubleshooting

| Issue | Quick Fix |
|-------|-----------|
| Mouse/keyboard not connecting | Replace batteries, try different USB port, re-sync receiver |
| Headset audio problems | Check connections, update audio drivers, try different device |
| Webcam not detected | Try different USB port, reinstall Logitech camera settings software |
| Controller drift | Clean around sticks with compressed air; contact support if persistent |
| Mouse double-clicking | Clean mouse sensor and buttons; contact support for replacement |

## Return Policy

- **30-day return window** from date of purchase
- Must be in original packaging with receipt
- Free returns for purchases from Logitech.com

## Automation Notes

### What we found:
- ⚠️ **No public repair request form** — All repairs go through chat or phone support
- ⚠️ **No online warranty check** — Requires account sign-in or contacting support
- ✅ **Standard HTML support pages** — Product selection works via clicking category tiles
- ✅ **Spare parts purchasable online** — `https://www.logitech.com/en-us/support/spare-parts`
- ✅ **No bot detection** — Support site is accessible
- ⚠️ **Shadow DOM on some pages** — Product category tiles use custom elements

### Automation approach:

**Recommended: Manual mode** — Guide user to contact Logitech via chat/phone since there is no self-service repair form.

1. Open `https://www.logitech.com/en-us/support`
2. Click the product category (Mice, Keyboards, Headsets, etc.)
3. Click "CHAT" or "PHONE" in the "GET ADDITIONAL ASSISTANCE" section
4. Describe the issue to the support agent

**If user insists on automation:**
- For warranty check: cannot automate — requires account access
- For repair: cannot automate — requires live support interaction

## Product Categories on Support Page

The main support page (`https://www.logitech.com/en-us/support.html`) has these product categories:
- GAMING (game controllers, racing wheels, etc.)
- HEADSETS AND EARPHONES
- KEYBOARDS
- MICE AND POINTERS
- MOBILE AND TABLET ACCESSORIES
- REMOTES AND SMART HOMES (Harmony)
- SPEAKERS AND SOUND SYSTEMS
- WEBCAMS, LIGHTS, AND CAMERA SYSTEMS

## References

- Support home: `https://www.logitech.com/en-us/support`
- Spare parts: `https://www.logitech.com/en-us/support/spare-parts`
- Register product: Via support page → "REGISTER A PRODUCT"
- Extend protection plan: Via support page link
- Phone support: 1-800-231-7717 (US)
