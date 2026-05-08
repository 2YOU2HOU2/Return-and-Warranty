---
name: sony-warranty
description: Sony & PlayStation device warranty & repair request flow. PS5, PS4, PlayStation VR, DualSense controllers.
version: 1.0.0
parent: find-warranty-and-repair-pages
metadata:
  manufacturer: Sony
  products: [PS5, PS4, PlayStation VR2, DualSense controller, PS Portal]
  portal_url: https://repairs.playstation.com/
  support_url: https://www.playstation.com/en-us/support/
---

# Sony Warranty & Repair (PlayStation)

## Quick Reference

| Resource | URL |
|----------|-----|
| **PlayStation Repairs** | `https://repairs.playstation.com/` |
| **Support hub** | `https://www.playstation.com/en-us/support/` |
| **PS5 System Info** | Settings → System → System Information → Serial Number |

## Repair Flow

**Portal**: `https://repairs.playstation.com/`  
**Navigation**: Products are organized by tab (Consoles / Controllers / VR Systems / Accessories).

### Step 1: Go to repair portal

```
https://repairs.playstation.com/
```

The page shows category tabs. Select **Consoles** for PS5/PS4.

### Step 2: Select your product

- **Consoles** tab → PlayStation®5 or PlayStation®4
- **Controllers** tab → DualSense, DualShock 4
- **VR Systems** tab → PlayStation VR2
- **Accessories** tab → PS Portal, charging stations, etc.

### Step 3: Product-specific page loads

The page shows:
- An image of the product
- Two buttons: **"It works"** (ends flow) and **"I still have the problem"** (required to proceed)

**Always click "I still have the problem"** to advance to troubleshooting.

### Step 4: Select issue category (dropdown)

A dropdown labeled **"What's the issue?"** appears. Options:

| Option | Use for |
|--------|---------|
| Error code issue | Specific error codes (CE-, NW-, etc.) |
| Power issue / console noise | No power, turns off, strange sounds |
| Crashing / freezing / corrupted save data | Game crashes, save file issues |
| **It's a video issue** | No video, black screen, HDMI problems |
| It's a system software issue | Update failures, corrupted software |
| It's a problem with the discs | Disc read errors, tray issues |
| I have a connection issue | WiFi, Bluetooth, internet |
| It's a pairing issue with disc drive | Disc drive not recognized |
| I have another issue | Anything not listed above (e.g., audio) |

### Step 5: Follow the issue path

After selecting a category, a second dropdown **"Select an Option"** narrows the issue.

#### Video Issue Path ("It's a video issue")

1. Select **"It's a video issue"** from first dropdown
2. Second dropdown options: "The HDMI cable doesn't work", "It's a picture problem", "It's a resolution issue", **"I have no image"**, "I have no HDR", "I have another issue"
3. Select **"I have no image"** for no-video scenarios
4. Page shows: HDMI port check → Yes/No (port damage = Yes → Request Repair)
5. HDMI cable check → Try different cable
6. Power indicator light check → Select your light color
7. Further troubleshooting steps accumulate
8. After exhausting steps → **"Request Repair"** button appears

#### Power Issue Path ("Power issue / console noise")

1. Select **"Power issue / console noise"** from first dropdown
2. Second dropdown options: "It turns off randomly", **"It has no power"**, "It's making strange noises"
3. For no power: select **"It has no power"**
4. Power indicator light check: **"There is no light"** (true no-power) or blinking color
5. Troubleshooting: try different outlet, try different cable, remove M.2 SSD
6. Safe Mode reinstall attempt → if fails → **"Request Repair"** button appears

#### Controller Path (Controllers tab)

1. Select **Controllers** tab
2. Select your controller model
3. Select issue: "The controller doesn't charge", "Audio / sound issue", "The controller won't connect", "Buttons/sticks not working", etc.
4. Follow troubleshooting → "Request Repair" when exhausted

### Step 6: Repair Request Form

After clicking **"Request Repair"**:

1. **Serial Number** — enter PS5 serial (Settings → System → System Information → Serial Number)
2. **Contact info** — name, email, phone
3. **Shipping address** — where to send/receive the console
4. **Problem description** — free text
5. **Submit** — receives confirmation email with tracking

## Product-Specific Notes

### PS5

- **Serial number location**: Settings → System → System Information → Serial Number (can't be remote)
- **Warranty**: 1-year manufacturer warranty from purchase date
- **PS5 Slim**: Same repair flow as standard PS5
- **Blinking white light**: Usually HDMI/display issue (console IS powering)

### PS4 / PS4 Pro

- Same repair portal, select PS4 instead of PS5
- Disc drive issues more common on PS4 Pro

### DualSense Controllers

- Controllers have separate tab — not under "Consoles"
- Common issues: drift, charging, audio
- Battery is not user-replaceable

### PlayStation VR2

- headset and controllers can be repaired separately
- Sensor tracking issues often require recalibration first

## Automation Notes

**This skill has been tested and confirmed working** with browser automation (Browserbase headless).

### Confirmed working paths:
- ✅ Video issue → I have no image → HDMI checks → power indicator → Request Repair
- ✅ Power issue → It has no power → There is no light → cable/unplug/M.2 → Safe Mode → Request Repair
- ✅ Power issue → It has no power → Blinking white → HDMI troubleshooting → Request Repair

### Known limitations:
- ⚠️ "I have another issue" path — dropdown selection may revert (known Oracle APEX bug)
- ⚠️ "It works" buttons use shadow DOM — `browser_click` on ref works reliably
- ⚠️ Ref numbers change between page loads — always take fresh snapshot before each action
- ⚠️ "CSS Error" modal may appear — if visible, expect automation failures

### Shadow DOM Navigation (Critical Timing Pattern)

The page uses Oracle APEX + LWC (Lightning Web Components) with **nested shadow DOM**. The dropdowns are inside `c-lwc-fr-combobox` → `c-lwc-fr-base-combobox` → shadow root.

**Nested shadow path for dropdowns:**
```
c-lwc-fr-troubleshooting → shadowRoot →
  c-lwc-fr-article[n] → shadowRoot →
    c-lwc-fr-combobox → shadowRoot →
      input[role=combobox]          ← click to open
      div[role=listbox]             ← options appear after click
        div[role=option]            ← click to select
```

**Critical timing sequence for dropdown selection:**
1. Click the `<input>` element (triggers dropdown to open)
2. **Wait ~2 seconds** — listbox options appear asynchronously
3. Query `div[role=listbox]` for options
4. Click the desired option

**Button navigation (different path):**
```
c-lwc-fr-troubleshooting → shadowRoot →
  c-lwc-fr-article[n] → shadowRoot →
    c-lwc-fr-button → shadowRoot →
      button                          ← native .click() works
```

**Rules:**
- Always use `browser_click` on ref from a fresh snapshot — ref numbers change between page loads
- The `article[n]` index increases by 1 after each successful selection — always re-index after advancing
- After clicking input, the listbox takes ~2s to populate — always wait before querying options
- Use `element.click()` inside `page.evaluate()` for real Chrome CDP; `dispatchEvent(MouseEvent)` does NOT trigger LWC handlers
- "CSS Error" modal may appear — dismiss it before continuing

```python
# Dropdown sequence (Playwright CDP or headless)
input_el.click()                          # open dropdown
time.sleep(2)                            # CRITICAL: wait for async listbox
options = listbox.query_selector_all('div[role=option"]')
options[desired_index].click()           # select option

# Button sequence
button = article_el.shadowRoot.querySelector('c-lwc-fr-button').shadowRoot.querySelector('button')
button.click()
```

## Power Indicator Diagnostic Rule

**Critical** for no-video reports:

| Light | Meaning | Route |
|-------|---------|-------|
| No light | Console has no power | Power issue → It has no power → There is no light |
| Blinking white | Console IS powering (HDMI issue) | It's a video issue → I have no image |
| Blinking blue | Hardware issue detected | Power issue → It has no power → Blinking blue → Request Repair |
| Solid blue | May be attempting to boot | Try normal boot, if fails → Power issue |
| Solid orange | Resting/charging mode | Boot normally |

**Rule**: ALWAYS ask about power light color before routing a "no video" report.

## Auto-Fill vs. Manual

When **"Request Repair"** appears:

**Ask**: *"Would you like me to auto-fill the form, or fill it yourself?"*

**Auto-fill**: Collect serial number + name/email/phone/address → fill form → submit

**Manual**: Give user the URL (`repairs.playstation.com`) and let them fill in their browser.

## Out-of-Warranty Repair Pricing (US, 2026)

| Repair | Out-of-Warranty (est.) |
|--------|----------------------|
| PS5 HDMI port | $150–$250 |
| PS5 power supply | $80–$150 |
| PS5 fan | $40–$80 |
| DualSense stick drift | $40–$60 |
| DualSense battery | $40–$60 |
| PS4 HDMI port | $100–$180 |
| PS4 power supply | $60–$100 |

*Prices are estimates through Sony authorized repair. Third-party shops often 30–50% cheaper. Contact Sony for a quote.*

## References

- Repair portal: `https://repairs.playstation.com/`
- PS5 warranty info: `https://www.playstation.com/en-us/support/articles/kA03M000000f0VaKAU/`
- PS5 error codes: `https://www.playstation.com/en-us/support/errors/ps5/`
