# IN-3590 - Satori: Prices for assets w/o SelectFeed coverage

**Type:** **Bug** | Feature | Exploration | Other
**Est:** 1h | **Confidence:** 65%

## Problem & Goal
Some assets in Satori's environment have stale prices. These cases are related to assets that are options or warrants, like Newhold Investment Corp III.

Set up the adapter to map the price from column H as the asset's price in cases when SelectFeed doesn't have a price coverage for these specialized instruments.

## Deliverables
- Enhanced Satori adapter that uses column H prices as fallback
- Logic to detect when SelectFeed doesn't have price coverage
- Price mapping functionality for options, warrants, and similar assets
- Validation that stale price issues are resolved for affected assets

## Entry Points
*Key components and systems to understand first*
- Current Satori adapter implementation and price mapping logic
- Column H data in Satori files - what prices are available there
- SelectFeed price coverage detection mechanism
- Assets affected: options, warrants (e.g., Newhold Investment Corp III)
- Current price staleness issues and identification process

## Plan
*High-level approach - bullet points preferred*
- Analyze current Satori adapter price mapping implementation
- Identify how SelectFeed coverage gaps are detected
- Review column H data structure and price information available
- Implement fallback price logic: SelectFeed price → Column H price if no SelectFeed coverage
- Test with known problematic assets (options, warrants like Newhold Investment Corp III)
- Validate that stale price issues are resolved
- Monitor adapter performance with new fallback logic

---

## Execution Notes
*Fill as you work - blockers, discoveries, pivots*

Figured out that we get the price, regardless of the asset, from column AQ on the file.
Asked Jorge about the issue. I may be confused myself, but Jorge says that the prices are coming from SelectFeed, and
that column AQ would be filled in if the SelectFeed price isn't given. Wouldn't that still result in an up-to-date price?
More to consider.

**Alex's Research and Resolution:**

Alex also did research on this issue and came to the following conclusion:

For background on the Newhold Investment Corp III holding, it looks like Satori instructions have a manual override, labeling all warrants as OTC instruments.

Since they are labeled OTC, we do not resolve them, and therefore, the price is defaulted to the source local price, which, for Satori, is column AQ along with FX rate.

**Three Options Considered:**
1. We continue manually overriding warrants to OTC and continue using the reported price (column AQ) as the price
2. We continue manually overriding warrants to OTC and use the UnitCostBase (column H) as their price (which is a bit confusing, as to why they'd prefer this)
3. We remove the manual override to OTC and instead allow the warrant to resolve, which will then allow SelectFeed to match it with an updated price

**Resolution:**
Jorge said that option 3 was the correct approach. Alex went through with implementation of the solution (which was removing the OTC specification).

### Themes

## Time Spent
**Actual:** 2.5h (Research: 2.5h | Implementation: 0h)

## Retrospective
**What went differently than planned?**

Task ended up being resolved by Alex through removing OTC manual override specification rather than implementing new price mapping logic. The issue was architectural rather than requiring new adapter functionality.

**Key learnings or gotchas:**

I did not know that the adapter took prices from SelectFeed during the process. I was under the assumption that the price listed in the positions file was what was put in the app, but we do actually supplement prices on our end. This is important context for understanding how price resolution works in the system.