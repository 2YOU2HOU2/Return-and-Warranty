# Logitech Support Site — Session Findings

## Key Discovery (2026-05-04)

Logitech does **not** have a self-service repair form. All warranty/repair requests go through live chat or phone. This makes it fundamentally different from Apple/Sony/HP/Google which have full self-service portals.

**URLs confirmed accessible:**
- `https://www.logitech.com/en-us/support` — main support portal (standard HTML, no bot protection)
- `https://www.logitech.com/en-us/support/spare-parts` — purchasable spare parts

**URLs confirmed 404:**
- `/warranty`, `/warranty-info`, `/rma`, `/repair` — no direct warranty/repair URLs exist
- `support.logi.com/hc/en-us/articles/360024820854-Warranty-Information` — article removed

**Product categories found on support page:**
- GAMING, HEADSETS AND EARPHONES, KEYBOARDS, MICE AND POINTERS
- MOBILE AND TABLET ACCESSORIES, REMOTES AND SMART HOMES
- SPEAKERS AND SOUND SYSTEMS, WEBCAMS, LIGHTS, AND CAMERA SYSTEMS

## Automation Feasibility

- Support page: ✅ Standard HTML, no bot detection
- Product category navigation: ✅ Works via `browser_click`
- Warranty check: ❌ No online tool exists
- Repair request form: ❌ Does not exist — must use chat/phone

**Conclusion:** For Logitech, Manual mode is the only viable path. Give user the support URL and direct them to CHAT or PHONE.
