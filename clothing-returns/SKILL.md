---
name: clothing-returns
description: General apparel return workflow for clothing brands. Covers ASOS, Nordstrom, Gap, Target, Macy's, Revolve, and other apparel retailers. Includes 30-day return window patterns, prepaid label flows, and in-store return options.
version: 1.0.0
parent: find-returns
metadata:
  type: catchall
  category: apparel
  return_window: "30 days (varies by retailer)"
---

# Clothing Returns — General Apparel Brands

## Overview

This is the **catch-all skill** for apparel retailers that don't have their own dedicated sub-skill. Most clothing brands follow a similar pattern: 30-day window, original payment refund, prepaid labels.

## Quick Reference: Major Apparel Retailers

| Retailer | Return Window | Return Fee | In-Store Return | Prepaid Label |
|----------|--------------|------------|----------------|---------------|
| **Nordstrom** | None (always) | Free | Yes | No — just bring item |
| **ASOS** | 28 days | Free | No | Yes (email) |
| **Gap/Old Navy/Banana Republic** | 30 days | Free | Yes | Yes |
| **Target** | 30 days | Free (Target RedCard: free) | Yes | Yes |
| **Macy's** | 30 days | Free | Yes | Yes |
| **Revolve** | 30 days | Free | Yes | Yes |
| **Saks Fifth Avenue** | 30 days | Free | Yes | Yes |
| **Neiman Marcus** | 30 days | Free | Yes | Yes |
| **Bloomingdale's** | 40 days | Free | Yes | Yes |
| **TJ Maxx/Marshalls** | 30 days | Free | Yes | No — bring to store |
| **Burlington** | 30 days | Free | Yes | No — bring to store |
| **J.Crew** | 30 days | Free | Yes | Yes |
| **Levi's** | 30 days | Free | Yes | Yes |
| **Patagonia** | 30 days | Free | Yes | Yes |
| **REI** | 1 year | Free | Yes | Yes |
| **L.L.Bean** | 1 year | Free | Yes | Yes |
| **Columbia** | 30 days | Free | Yes | Yes |
| **Under Armour** | 30 days | Free | Yes | Yes |
| **Lululemon** | 30 days | Free | Yes | Yes |
| **Athleta** | 60 days | Free | Yes | Yes |

## Standard 30-Day Return Workflow

### Step 1: Find Your Receipt / Order Confirmation

- **Original receipt**: Physical or digital
- **Order confirmation email**: Search inbox for retailer name + "order confirmation"
- **Account order history**: Sign into retailer's website

### Step 2: Check Return Window

- Standard: 30 days from delivery date
- Start date = when item was delivered, not when ordered
- Holiday extended windows: Many retailers extend to Jan 31 for holiday purchases

### Step 3: Inspect Item Condition

Must be:
- Unworn / unwashed
- Tags still attached
- Original packaging (shoe boxes, etc.) preferred

Exceptions that are **always returnable**:
- Defective items (even without tags)

Items that are **typically non-returnable**:
- Swimwear / underwear (hygiene)
- Earrings / pierced jewelry
- Personalized items
- Final sale / clearance items

### Step 4: Choose Return Method

**By Mail (Prepaid Label):**
1. Sign into account → Orders → Start return
2. Select items + reason
3. Email receives prepaid label
4. Pack + ship

**In-Store Return:**
1. Bring item with confirmation
2. Get refunded immediately
3. No printing or shipping needed

### Step 5: Pack Securely

- Use original packaging if available
- Include all original tags, accessories, inserts
- Seal box securely

### Step 6: Drop Off / Ship

- Drop at carrier location (UPS, USPS, FedEx)
- Or drop at store if retailer accepts own returns

### Step 7: Track Refund

- Refund to credit card: 5–10 business days after delivery
- Refund to store credit: Immediate
- Cash (in-store): Immediate

## Nordstrom — Special Case

**No return window — ever.** Nordstrom has one of the most generous return policies in retail:

- **No time limit** on returns
- **No receipt required** (can look up by card or phone number)
- **Any reason** — wrong size, changed mind, defects
- **Any method** — mail or any Nordstrom store

**Automation note:** Nordstrom makes returns extremely easy. You can initiate a return online or just walk into any Nordstrom with the item.

## ASOS — 28 Days

| Detail | Info |
|--------|------|
| Window | 28 days from delivery |
| Sign-in required | Yes |
| Prepaid label | Yes (emailed) |
| In-store return | No |
| Final sale items | Non-returnable |

**URL:** `https://www.asos.com/us/orders/`

## Gap / Old Navy / Banana Republic / Athleta

All owned by Gap Inc. Same return flow:

1. Sign into account at respective website
2. Go to Orders → Start return
3. Select items + reason
4. Prepaid label emailed (UPS)
5. Drop at UPS or Old Navy/Gap accepts Gap Inc. brand returns at any Gap Inc. store

## Target

| Detail | Info |
|--------|------|
| Window | 30 days (15 days for electronics: Apple, Dyson, etc.) |
| Sign-in required | Preferred but not strictly required |
| Prepaid label | Yes — email or Target app |
| In-store return | Yes — bring item to any Target |
| Drop-off | UPS, FedEx, or Target store |

**Special:** Target RedCard holders get **free return shipping** on all orders.

## Revolve

| Detail | Info |
|--------|------|
| Window | 30 days (extended to 60 days for first-time buyers) |
| Sign-in required | Yes |
| Prepaid label | Yes (emailed) |
| In-store return | Yes — Revolve has a "Revolve at Nordstrom" partnership |
| Free returns | Always free |

## TJ Maxx / Marshalls

| Detail | Info |
|--------|------|
| Window | 30 days with receipt |
| Sign-in required | No |
| Prepaid label | No — in-store return only |
| In-store return | Yes — any TJ Maxx or Marshalls |
| Receipt required | Yes — must have original receipt |

**Note:** TJ Maxx/Marshalls do NOT accept mail-in returns. Must return to a physical store with receipt.

## Common Return Reasons (All Retailers)

| Reason Code | Description | Typical Fee |
|------------|-------------|-------------|
| Doesn't fit | Size doesn't suit | Free (most retailers) |
| Not as expected | Different from website photo | Free |
| Defective | Broken, missing parts, damaged | Free |
| Wrong item | Sent wrong product | Free |
| Changed mind | No longer want | Free (most retailers) |
| Late delivery | Arrived after needed | Varies |

## What Blocks Automation for Most Apparel Sites

| Blocker | Severity |
|---------|---------|
| Account sign-in required | High — most return flows need auth |
| Anti-bot/WAF on fashion sites | Medium-High — many fashion retailers use Cloudflare/WAF |
| Order-specific session tokens | Medium — can't construct return URLs directly |
| CAPTCHA on some sites | Low-Medium — usually only on failed login attempts |
| JS-heavy SPA navigation | Low-Medium — most modern apparel sites are SPA |

### High-Automation-Risk Retailers (bot-blocked)

These retailers have aggressive anti-bot protection and likely need manual mode:
- **Zara** — EdgeSuite/Akamai WAF, silent block
- **H&M** — Cloudflare, silent block
- **ASOS** — Cloudflare, CAPTCHA likely

### Medium-Automation-Risk Retailers

These typically work in headless but may show CAPTCHA:
- **Gap/Old Navy** — Standard web properties
- **Macy's** — Standard web properties
- **Nordstrom** — Standard web properties
- **Target** — Standard web properties

## Automation Decision Tree

```
Is the retailer a dedicated sub-skill (amazon, zara, hm)?
├── YES → Use that sub-skill
└── NO → Use this clothing-returns skill
      ├── Is retailer on the "high risk" list?
      │   ├── YES → Manual mode only
      │   └── NO → Try auto-fill first
      └── Try browser automation:
          1. Navigate to retailer's account/orders page
          2. Sign in if needed
          3. Find "Start return" or "Return items"
          4. Select items + reason
          5. Check if prepaid label generates
          6. If blocked at any step → switch to manual
```

## Generic Step-by-Step (When No Sub-Skill Exists)

### For Auto-Fill:

1. **Search for retailer order history URL pattern:**
   - `{retailer}.com/orders`
   - `{retailer}.com/account/orders`
   - `{retailer}.com/my-account/returns`

2. **Navigate to return center:**
   - Try `https://www.{retailer}.com/returns`

3. **Sign in** if required

4. **Locate order** — search by order number, email, or date range

5. **Select return** — checkboxes for items, dropdown for reason

6. **Generate label** — confirm and look for email with prepaid label

7. **Confirm** — note tracking number and expected refund date

### For Manual Mode:

Give user:
1. Retailer account URL
2. Specific steps to find return initiation
3. What to expect (prepaid label, in-store option, refund timeline)
4. Any retailer-specific quirks

## Return Policy Red Flags

| Warning Sign | What It Means |
|-------------|---------------|
| "Final sale" on receipt | Item cannot be returned |
| "No returns without tags" | Must have original tags attached |
| "15-day window" | Electronics often have shorter windows |
| "Exchange only" | Some retailers only offer exchanges, not refunds |
| "Store credit only" | Some clearance items only refund to gift card |
| "Restocking fee" | Electronics/appliances may charge 15–20% restocking fee |

## Best Buy Return Policy (Electronics Reference)

| Category | Window | Notes |
|----------|--------|-------|
| Most items | 15 days | Standard |
| Apple products | 15 days | Through Best Buy |
| Major appliances | 15 days | Must be pre-arranged |
| Cell phones | 15 days | With carrier return policy |
| Gaming consoles | 15 days | Opened or unopened |

## Walmart Apparel Return Policy

| Category | Window | Notes |
|----------|--------|-------|
| Most apparel | 90 days | With receipt |
| Womenswear | 90 days | Generous window |
| Shoes | 90 days | With receipt |
| Jewelry | 90 days | With receipt |

**Note:** Walmart has a **90-day** return window for most apparel — much longer than the standard 30 days.

## References

- Nordstrom returns: `https://www.nordstrom.com/returns`
- ASOS returns: `https://www.asos.com/us/orders/`
- Gap returns: `https://www.gap.com/returns`
- Target returns: `https://www.target.com/returns`
- Revolve returns: `https://www.revolve.com/returns`
- TJ Maxx returns: In-store only
