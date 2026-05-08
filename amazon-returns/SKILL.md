---
name: amazon-returns
description: Amazon return request flow — initiate returns, print prepaid labels, track refunds for marketplace and direct Amazon purchases.
version: 1.0.0
parent: find-returns
metadata:
  retailer: Amazon
  website: amazon.com
  return_window: 30 days (most items)
  sign_in_required: true
  category: marketplace
---

# Amazon Returns

## Quick Reference

| Resource | URL |
|----------|-----|
| **Return Center** | `https://www.amazon.com/returns` |
| **Order History** | `https://www.amazon.com/gp/your-account/order-history` |
| **Sign In** | `https://www.amazon.com/ap/signin` |

## Return Policy

| Item Type | Return Window | Notes |
|-----------|--------------|-------|
| Most items | 30 days from delivery | Standard |
| Clothing | 30 days | Must have tags |
| Electronics | 30 days | Must be unopened |
| Furniture | 30 days | Must be assembled |
| Fresh flowers | Non-returnable | Final sale |
| Gift cards | Non-returnable | Final sale |
| Open software | Non-returnable | Final sale |
| Final sale items | Non-returnable | Check listing |

**Amazon Marketplace (third-party sellers):** May have different return windows. Check listing page for seller-specific policy.

## Return Reasons (Standard Codes)

| Reason | Shipping Fee |
|--------|-------------|
| Wrong item received | Free |
| Defective/Damaged | Free |
| Changed mind | Usually paid by buyer |
| Better price found | Usually paid by buyer |
| Doesn't fit (clothing) | Usually paid by buyer |
| Not as described | Free |
| Arrived too late | Varies |

## Return Flow

### Step 1: Sign In (REQUIRED)

Go to `https://www.amazon.com/returns` — immediately redirects to sign-in.

**Automation note:** This is the primary blocker. Without valid Amazon credentials and an active session, the return flow cannot be automated.

If you have credentials:
1. Navigate to `https://www.amazon.com/returns`
2. Sign in with email + password
3. Complete any CAPTCHA if presented

### Step 2: Select Item to Return

After sign-in, you land on the Return Center. Options:

**Option A — Search for order:**
1. Type order number or search by keyword
2. Find the item from your order history

**Option B — Browse orders:**
1. Click "Return or replace items"
2. Select from recent orders

### Step 3: Choose Return Reason

1. Select the item(s) to return (checkbox)
2. Choose return reason from dropdown:
   - Wrong item was sent
   - Item defective/damaged
   - No longer needed
   - Changed my mind
   - Item too small/small fit
   - Item too large/large fit
   - Not as described
   - Other (specify)
3. Add optional comments
4. Click **Continue**

### Step 4: Choose Return Method

**For Defective/Wrong Item:**
- Free return shipping provided automatically
- Prepaid label emailed

**For Changed Mind:**
- May need to pay for return shipping
- Option to drop off at Amazon Locker or Kohls

### Step 5: Choose Refund Method

| Method | Processing Time |
|--------|----------------|
| Original payment method | 5–7 business days |
| Amazon gift card | Immediate |
| Refund to different payment | 5–7 business days |

### Step 6: Print Label / Get QR Code

- Prepaid label sent via email
- Or show QR code at UPS/USPS/drop-off location
- Pack item securely with original packaging if possible

### Step 7: Ship and Track

- Drop off at carrier or scheduled pickup
- Amazon sends confirmation when return is received
- Refund processed within 5–10 business days after delivery

## Amazon Locker & Kohls Drop-Off

**Amazon Locker:**
- Select at return initiation
- Get a pickup code
- Drop at any Amazon Locker within 3 days
- No label printing needed — QR code at locker

**Kohls:**
- Amazon offers free Kohls drop-off for returns
- Bring item and QR code to any Kohls
- Kohls packs and ships for you (no box needed)

## Common Issues

| Issue | Solution |
|-------|----------|
| Return window expired | Amazon may offer partial refund as gift card — contact support |
| Lost return label | Go to Returns Center → find order → request new label |
| Item shipped but not delivered | Wait until marked delivered before initiating |
| Wrong item delivered | Select "wrong item" reason — free return + resend correct item |
| Marketplace seller won't respond | Amazon A-to-Z guarantee may apply — file claim |
| Item arrived damaged | Photo evidence may speed up refund — contact support |

## Automation Notes

### What Works in Browserbase Headless

| Step | Automatable | Notes |
|------|-------------|-------|
| Sign-in page | ❌ | Requires credentials + session cookies |
| Return Center landing | ❌ | Blocked by auth |
| Form fields | ⚠️ | Cannot test without auth |
| Label generation | ⚠️ | Cannot test without auth |

### What Blocks Automation

1. **Authentication wall** — Must be signed in with valid Amazon account
2. **Session cookies** — Return flow requires active session
3. **CAPTCHA** — May appear on suspicious login activity
4. **Bot detection** — Amazon uses behavioral analysis

### Automation Approach

**Manual mode is the only reliable option for Amazon returns.**

1. Open `https://www.amazon.com/returns`
2. Sign in with credentials
3. Follow the return wizard
4. Print label or show QR code at drop-off

## Auto-Fill vs Manual

- **Auto-fill**: Not feasible — auth wall cannot be bypassed
- **Manual**: Full step-by-step instructions provided above

## References

- Return Center: `https://www.amazon.com/returns`
- Order History: `https://www.amazon.com/gp/your-account/order-history`
- Help: `https://www.amazon.com/gp/help/customer/Returns.html`
