# IN-3590 - Satori: Prices for assets w/o SelectFeed coverage

**Type:** Bug | **Feature** | Exploration | Other
**Est:** [X]h | **Confidence:** [X]%

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

### Themes

## Time Spent
**Actual:** [X]h (Research: [X]h | Implementation: [X]h)

## Retrospective
**What went differently than planned?**

**Key learnings or gotchas:**