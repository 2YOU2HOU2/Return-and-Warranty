---
name: find-warranty-and-repair-pages
description: Navigate corporate support sites to locate warranty claims, repair requests, and RMA flows for electronics and appliances. Umbrella skill — see sub-skills for manufacturer-specific flows.
version: 2.0.0
metadata:
  hermes:
    tags: [support-site, warranty, repairs, RMA, corporate-navigation]
    related_skills: [web-bot-protection-guide, web-scraping-blocked-alternatives, warranty-check]
    sub_skills: [sony-warranty, apple-warranty, samsung-warranty, microsoft-warranty, nintendo-warranty, lg-warranty, dell-warranty, hp-warranty, google-warranty, logitech-warranty]
---

# Find Warranty & Repair Pages (Umbrella)

## Overview

This is the **umbrella skill** for electronic device warranty and repair request automation. It provides shared patterns, anti-bot strategies, form-filling templates, and coordinates manufacturer-specific sub-skills.

**Sub-skills (one per manufacturer):**
- `sony-warranty` — PlayStation consoles, Sony electronics
- `apple-warranty` — iPhone, Mac, iPad, Apple Watch, AirPods
- `samsung-warranty` — phones, tablets, TVs, home appliances
- `microsoft-warranty` — Xbox, Surface, Windows devices
- `nintendo-warranty` — Switch, Joy-Con, game cards
- `lg-warranty` — phones, appliances, TV, audio
- `dell-warranty` — XPS, Latitude, Alienware, desktops (⚠️ bot-blocked)
- `hp-warranty` — printers, laptops, desktops, monitors
- `google-warranty` — Pixel phones, Pixel Watch, Pixel Buds
- `logitech-warranty` — mice, keyboards, headsets (⚠️ **no self-service form** — repairs via chat/phone only)

**Umbrella responsibilities:**
1. Shared browser/automation patterns that apply across all manufacturers
2. Generic repair form template (serial number, address, payment, etc.)
3. Shipping and Returns information common to all warranty flows
4. Anti-bot mitigation strategies (Oracle APEX, Arkose Labs, Cloudflare)
5. Route users to the correct manufacturer sub-skill based on their device

## Workflow

### Step 1: Identify the manufacturer

Ask the user: *"What brand is your device?"*

Route to the appropriate sub-skill. If the manufacturer isn't yet covered, use this umbrella's generic navigation approach to discover the repair flow.

### Step 2: Load the manufacturer sub-skill

```python
skill_view(name='{manufacturer}-warranty')
```

### Step 3: Follow the sub-skill's repair flow

Each sub-skill defines:
- The repair portal URL
- Product category navigation
- Issue path dropdowns
- Known automation quirks

### Step 4: Auto-Fill or Manual?

When the repair request form appears, ask the user:
> *"Would you like me to auto-fill the form, or would you prefer to fill it yourself?"*

- **Auto-fill**: Collect serial number + contact/shipping info, fill and submit
- **Manual**: Give user the URL and let them fill in their own browser

## Shared Anti-Bot Patterns

### Oracle APEX + Shadow DOM (PlayStation, many electronics)

**Symptom**: Dropdown clicks register (`success: true`) but selection reverts immediately.

The site renders controls inside **shadow DOM** inaccessible from `browser_console` JS. The `browser_click` tool works on the Playwright side — use it directly rather than JS `dispatchEvent`.

```python
# CORRECT: use browser_click on the option ref from snapshot
browser_click(ref='e35')  # option element ref

# WRONG: browser_console JS cannot pierce shadow DOM
browser_console(expression='document.querySelector(...).click()')
```

### Arkose Labs / Bot Protection Ifames

Many warranty sites load bot protection scripts in hidden iframes. These don't block automation directly but may flag the session if abused.

**Mitigation:**
- Use `playwright-stealth` (`from playwright_stealth import Stealth`) when launching a fresh session
- Add `--disable-blink-features=AutomationControlled` via browser args
- Avoid rapid repeated requests to the same endpoint

### Cloudflare (Streaming sites, some electronics)

When Cloudflare Ray ID appears, use `playwright-stealth`:
```python
from playwright_stealth import Stealth
with Stealth().use_sync(sync_playwright()) as p:
    browser = p.chromium.launch(args=['--disable-blink-features=AutomationControlled'])
```

See also: `cloudflare-bypass-playwright-stealth` skill.

## Generic Repair Form Template

When a manufacturer-specific form is reached, these fields are common across most warranty/repair flows:

| Field | Notes |
|-------|-------|
| Serial number | Found on device back/bottom, or in Settings → System |
| Product model | May be pre-filled from serial |
| Name / Email | Account holder |
| Phone | Mobile preferred for shipping updates |
| Shipping address | Where to send the repaired/replacement device |
| Purchase date | For warranty validity check |
| Problem description | Free text or dropdown |
| Proof of purchase | Photo upload (receipt, invoice) |

**Serial number location by device type:**
- iPhone: Settings → General → About → IMEI, or SIM tray
- Android: Settings → About phone → IMEI, or Settings → Connections → About phone
- Mac: Apple menu → About This Mac → Serial Number
- PS5: Settings → System → System Information → Serial Number
- Xbox: Settings → System → Console info → Serial number
- Nintendo Switch: Settings → Console → Serial Number

## Shipping & Returns (Common Across All)

Most warranty repairs follow this pattern:

1. **Device received** → inspection (3–5 business days)
2. **In-warranty repair** → free repair, return shipping label provided
3. **Out-of-warranty** → fee quoted before repair, must approve
4. **Keep or return** — ask user preference for replaced units

**User questions to answer:**
- *"How long does it take?"* — typically 7–14 business days total
- *"Is it free?"* — depends on warranty status + issue type
- *"What do they do with my data?"* — advise factory reset before sending

## Reference: Sub-Skill Conventions

Each manufacturer sub-skill follows this structure:

```
{manufacturer}-warranty/
├── SKILL.md                  ← main skill (this file's convention)
└── references/
    └── repair-pages.md        ← manufacturer-specific URL directory
```

### SKILL.md frontmatter:

```yaml
---
name: {manufacturer}-warranty
description: {manufacturer} device warranty & repair request flow
version: 1.0.0
parent: find-warranty-and-repair-pages
metadata:
  manufacturer: {name}
  products: [product categories covered]
  portal_url: {repair portal URL}
---
```

## Troubleshooting

| Problem | Solution |
|---------|----------|
| URL returns 404 | Corporate sites use SPA navigation — navigate through UI, don't guess sub-URLs |
| No "Repairs" link visible | Look under "Hardware & Repairs", "Device Service", or "Protect Your Device" |
| Page reloads to 404 | Repair flow may be on a separate subdomain |
| "Sign in required" | Warranty claims often require linking device to account first |
| Dropdown reverts after selection | Shadow DOM issue — use `browser_click` on option ref, not JS dispatch |
| Click succeeds but page doesn't advance | Oracle APEX state machine — try Manual mode |

## Key Takeaway

> When looking for warranty/repair pages on corporate sites, **navigate down through categories** rather than guessing URLs horizontally. The repair infrastructure is often on a separate subdomain and direct URLs are not discoverable via guesswork.
