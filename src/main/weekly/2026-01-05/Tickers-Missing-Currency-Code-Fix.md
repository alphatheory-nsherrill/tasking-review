# Tickers With No Currency Code

**Type:** **Bug** | Feature | Exploration | Other
**Est:** [X]h | **Confidence:** [X]%

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

### Themes

## Time Spent
**Actual:** [X]h (Research: [X]h | Implementation: [X]h)

## Retrospective
**What went differently than planned?**

**Key learnings or gotchas:**