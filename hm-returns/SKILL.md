---
name: hm-returns
description: H&M return request flow for online purchases — return by mail or in-store, prepaid labels, refund timeline.
version: 1.0.0
parent: find-returns
metadata:
  retailer: H&M (Hennes & Mauritz)
  website: hm.com
  return_window: 30 days from delivery
  sign_in_required: true
  category: apparel
---

# H&M Returns

## Quick Reference

| Resource | URL |
|----------|-----|
| **H&M Returns** | `https://www2.hm.com/en_us/returns.html` |
| **H&M Account** | `https://www.hm.com/us/en/account` |
| **Order History** | Via account page |
| **Store Locator** | `https://www.hm.com/us/en/store-locator` |

## Return Policy

| Condition | Details |
|-----------|---------|
| **Return window** | 30 days from delivery date |
| **Receipt required** | Yes — order confirmation email or account order history |
| **Item condition** | Unworn, unwashed, with original tags attached |
| **Packaging** | Original bag or packaging preferred |
| **Refunds** | Original payment method |

**Exceptions:**
- Lingerie, swimwear, underwear: Non-returnable for hygiene reasons
- Personalized/customized items: Non-returnable
- Beauty products: Non-returnable if sealed
- Final sale items: Check listing — may be non-returnable

## Return Methods

H&M offers **two return options** for online purchases:

### Option 1: Return by Mail (Prepaid Label)

1. Sign into your H&M account
2. Go to "Orders" → select the order to return
3. Select items and return reason
4. H&M emails a prepaid return label
5. Pack item and print label
6. Drop off at any USPS, UPS, or FedEx location

**Cost:** Free for all returns (H&M provides prepaid label)

### Option 2: Return In-Store

1. Bring the item(s) to any H&M US store
2. Show order confirmation (digital or print)
3. Item refunded immediately to original payment method

## Return Flow (Online — By Mail)

### Step 1: Sign In to H&M Account

Go to `https://www.hm.com/us/en/account`

**Automation note:** Sign-in is required. Cannot access return flow without account.

### Step 2: Select Order

1. Go to "Orders" section
2. Find the order containing the item to return
3. Click "Return" or "Start return"

### Step 3: Select Items and Reason

1. Check the box next to each item to return
2. Select return reason from dropdown:
   - Doesn't fit
   - Not as expected / Different from website
   - Defective/Damaged
   - Wrong item received
   - Changed my mind
   - Other
3. Click **Continue**

### Step 4: Confirm Return

1. Review return details
2. Confirm — H&M emails prepaid return label + QR code
3. Print label OR use QR code at drop-off

### Step 5: Pack and Ship

1. Pack item securely with all original packaging
2. Attach printed label OR show QR code on phone at carrier location
3. Drop off at USPS, UPS, or FedEx location

### Step 6: Refund

- Refund processes within 5–7 business days after H&M receives the item
- Credit card: Allow 1–2 billing cycles for refund to appear
- Original payment method only

## Return Reasons and Fees

| Reason | Return Fee |
|--------|-----------|
| Doesn't fit | Free |
| Wrong item received | Free |
| Defective/Damaged | Free |
| Changed mind | Free |
| Not as described | Free |

**Note:** H&M offers **free returns** for all online purchases.

## In-Store Return Process

1. **Gather items** — ensure items have tags and are unworn
2. **Bring confirmation** — show digital order confirmation on phone or print it
3. **Visit any H&M US store** — no carrier drop-off needed
4. **Get refund** — processed immediately to original payment method

## Common Issues

| Issue | Solution |
|-------|----------|
| No carrier location nearby | Use in-store return at any H&M location |
| Lost confirmation email | Log into H&M account to retrieve order details |
| Return window expired | Contact H&M customer service — may offer store credit |
| Item without tags | H&M may refuse return; contact customer service |
| Final sale item | Check listing — may be non-returnable |
| Need exchange | H&M doesn't offer direct exchanges — return for refund and reorder |

## Automation Notes

### What Blocks Automation

| Blocker | Details |
|---------|---------|
| **Aggressive WAF/Cloudflare** | H&M uses Cloudflare or similar WAF that blocks headless browsers |
| **Sign-in required** | Must be authenticated to access orders |
| **No guest returns** | Cannot initiate return without account |
| **Silent block** | Blocks before presenting CAPTCHA |

### Attempted Workarounds (Failed)

- Direct URL access: ❌ Access Denied
- Mobile site (m.hm.com): ❌ Access Denied
- Google cached pages: ❌ Cloudflare CAPTCHA
- Wayback Machine: ❌ No archived snapshots of returns page
- Search aggregators: ❌ Also blocked by Cloudflare

### Automation Approach

**Manual mode is required for H&M.**

1. Open `https://www.hm.com/us/en/account` in a real browser
2. Sign in with credentials
3. Navigate to Orders → Start return
4. H&M emails prepaid label
5. Drop off at USPS/UPS/FedEx or return to H&M store

## Auto-Fill vs Manual

- **Auto-fill**: Not feasible — WAF blocks headless browsers, auth wall requires session
- **Manual**: Full step-by-step instructions provided above

## H&M vs Other Retailers

| Feature | H&M | Zara | ASOS |
|---------|-----|------|------|
| Return window | 30 days | 30 days | 28 days |
| Return fee | Free | Free | Free |
| Prepaid label | Yes (email) | Yes (email) | Yes (email) |
| In-store return | Yes | Yes | No |
| Sign-in required | Yes | Yes | Yes |
| Carrier options | USPS/UPS/FedEx | UPS only | Yodel/Hermes |

## References

- H&M returns: `https://www2.hm.com/en_us/returns.html`
- H&M account: `https://www.hm.com/us/en/account`
- Store locator: `https://www.hm.com/us/en/store-locator`
- Customer service: Via chat on website or 1-800-xxx (see website)
