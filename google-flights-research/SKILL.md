---
name: google-flights-research
description: Research flight prices using browser automation with Google Flights. Reliable for verifying conflicting price data and getting up-to-date nonstop fares.
---
# Google Flights Browser Research Skill

## When to use
Research flight prices, options, and schedules using browser automation. Use this when web search / delegate_task approaches return stale, wrong, or conflicting price data — direct browser verification is more reliable.

## Approach

### Reliable method: Direct Google Flights URLs
Construct URLs manually instead of trying to fill interactive forms. This avoids combobox timeout issues and bot detection.

**URL pattern:**
```
https://www.google.com/travel/flights?q={ORIGIN}+to+{DEST}+{DATE}+one+way+nonstop&curr=USD
```

Examples:
- `https://www.google.com/travel/flights?q=ORD+to+LAX+May+14+2026+one+way+nonstop&curr=USD`
- `https://www.google.com/travel/flights?q=LAX+to+ORD+May+19+2026+one+way+nonstop&curr=USD`

For **round trip**, use the `tfs=` parameter or use Google Flights' round-trip mode by omitting "one way".

### What to look for in the snapshot
- `tab "Cheapest from $XX"` — cheapest nonstop price
- `link "From $XX US dollars. Nonstop flight with {AIRLINE}."` — individual flight results
- `textbox "Departure"` — verify the correct date loaded
- `alert: N results returned.` — confirms search worked

### Browsing multiple dates quickly: Date Grid tool
The **"Date grid" button** in the Price insights section is the fastest way to compare prices across many dates without reloading the page.
- Click `button "Date grid"` to open a calendar modal showing prices for each day
- Use `button "Scroll left"` / `button "Scroll right"` to navigate months
- Click any date button (e.g. `$97`) to select that departure date and reload results
- Use `button "Cancel"` to close without changing
- Note: only shows ~7-9 days visible at a time, so multiple scrolls needed for full month

### Internal API (unreliable for per-day prices)
The endpoint `https://www.google.com/travel/flights/r/api/search?year=2026&month=5&day=X&...` returns ~1.8MB of data per request but extracting reliable per-day prices is difficult — regex for "nonstop" prices returned $56 for every day in May, which is incorrect. Do not rely on this for comparing prices across dates.

### Changing the departure date via browser
The date picker combobox (`textbox "Departure"`) is hard to interact with programmatically — ref IDs are unstable across renders. Two alternatives:
1. Use the **Date Grid** modal to click a specific date
2. Use direct URL construction: `https://www.google.com/travel/flights?q=ORD+to+LAX+May+15+2026+one+way+nonstop`

### Pitfalls
- **Kayak**: Blocks automated browsers aggressively — do not use
- **Form interaction**: Trying to type into comboboxes/fields often times out — prefer URL-based navigation
- **Subagent delegation**: Can return inaccurate or outdated price data for flight searches — always verify with browser
- **Price variance by date**: Mid-week dates (Tue/Wed) are often cheapest for returns; Thursdays are cheapest for outbound on this route
- **Nonstop filter**: Append `nonstop` to URL or click the filter in the UI
- **Internal API prices**: The `r/api/search` endpoint data is not reliably parseable for price comparison across dates — use the browser Date Grid instead

## Verification steps
1. Confirm the date in `textbox "Departure"` matches your target
2. Confirm `Nonstop` filter is selected
3. Check `Cheapest from $XX` tab for the lowest price
4. Note airline, time, and bags included — prices on basic economy carriers (Frontier, Spirit) often exclude bags
