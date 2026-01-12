# Tickers With No Currency Code

**Type:** **Bug** | Feature | Exploration | Other
**Est:** 3h | **Confidence:** 60%

## Problem & Goal
All tickers need a Currency Code.

Query shows tickers missing currency codes:
```sql
SELECT tickerId, name, currencyCode, currencysymbol,selectfeedticker, bloombergTicker, description, active, created, modified
FROM ticker
WHERE currencyCode is null and selectfeedticker is not null and (active = 1 or active is null)
```

Seems that an adapter is pulling an existing ticker without a currency code, and is meaning to set currency code, but failing.

## Deliverables
- Fix for TickerFactoryForIdmServicesGuidepost to properly set currencyCode
- Validation that existing null currencyCode tickers get updated
- Ensure adapter properly sets currency code for new/updated tickers

## Entry Points
*Key components and code to understand first*
- `TickerFactoryForIdmServicesGuidepost` - specifically the `applyTickerChanges` function
- SQL query results showing affected tickers
- Adapter logic that should be setting currency codes
- Ticker database schema and currency code requirements

## Plan
*High-level approach - bullet points preferred*
- Review TickerFactoryForIdmServicesGuidepost.applyTickerChanges function
- Identify why currencyCode is not being included in the logic
- Fix the applyTickerChanges function to properly handle currencyCode
- Test fix with sample tickers
- Run query to validate existing null currencyCode tickers get updated
- Verify adapter behavior for new ticker creation/updates

---

## Execution Notes
*Fill as you work - blockers, discoveries, pivots*

Upon investigation, it turns out that the new TickerFactoryForIdmServicesGuidepost was not including currencyCode in the actual logic of the applyTickerChanges function.

Went through the guidepost's ticker update functionality and ensured all relevant fields were being updated. This turned
into a review with Dan about how the system handles Figi vs Composite Figi.

### Themes

This was a good introduction to the new Guidepost ticker update system. I took some extra time to review the component,
and really learn how the pieces fit together. This system is definitely an upgrade over the ticker factory merge in
system from before.

## Time Spent
**Actual:** 2.5h (Research: 2h | Implementation: .5h)

## Retrospective
**What went differently than planned?**

A larger review on the concept of Figi vs Composite Figi, and when to use each was held. This was not in the immediate
scope of the issue, but what necessary to ensuring completeness of the component.

**Key learnings or gotchas:**

The new code that was causing an issue was technically correct with the other ticker fields it was updating. This 
highlights a need for stricter review strategies.