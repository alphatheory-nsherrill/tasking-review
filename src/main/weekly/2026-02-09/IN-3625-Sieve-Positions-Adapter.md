# IN-3625 - Sieve Positions Adapter

**Type:** Feature  
**Est:** 4h | **Confidence:** 70%  
Completed: [ ]

## What / Why / For Whom / How
- **What:** Create and document the Sieve Capital positions adapter mapping for the AlphaTheory positions CSV feed.
- **Why:** Ensure positions ingest correctly with accurate identifiers, security types, and fund value calculations.
- **For Whom:** AlphaTheory operations and downstream consumers relying on IDM position data.
- **How:** Map CSV columns to adapter fields, add instrument-type conditionals, and configure FX and fund mapping rules.

## Deliverables
Adapter configuration for `SieveCapitalAlphaTheoryPositionsExternalAppInstructionsContainer` plus mapping rationale and field usage summary.

## Entry Points
- `com.alphatheory.service.externalapp.instructions.SieveCapitalAlphaTheoryPositionsExternalAppInstructionsContainer`
- Source file pattern `ALPHATHEORY_POSITIONS_YYYYMMDD.csv`
- Sample file columns: Date, Entity Name, Instrument Name/Type, identifiers, quantities, TD market values

## Plan
- Review CSV format and column inventory
- Define field mappings (shares, price, identifiers, report date, currency)
- Add conditionals for security type and ticker treatment based on Instrument Type
- Configure FX rate resolution and fund mapping using Entity Name
- Specify fund value calculation (sum of TD long + TD short market values)
- Capture test checklist

---

## Execution Notes
- Analyzed CSV structure: 25 columns, UTF-8, trade-date quantities and market values.
- Identified mapping strategy: use TD quantities/values, map identifiers (SEDOL/ISIN/CUSIP), map Instrument Name to custom symbol.
- Initial AI MCP-assisted review introduced faulty assumptions, so I took a brief detour to review type mappings.
- Confirmed there is no valid AlphaTheorySecurityType for ETF; ETFs are typically mapped as `common_stock`.
- Established conditional logic: Common Equity -> common_stock, ETF -> common_stock; both use primaryExchangeInstrument treatment.
- Set fund mapping to Entity Name and fund value to sum of TD long + TD short market values.
- Added FX rate resolution with default USD.

## Validation / Execution
**Tuesday 11PM Update:** John added department settings in production. However, discovered that production->staging synchronization occurs at 9PM, so the changes weren't captured for Wednesday testing. Learned from Mike that sync timing prevented availability of fund/etc for Sieve testing. Mike delayed synchronization to 11PM as a courtesy gesture. Department settings should be available for testing and production deployment Thursday morning.

**Testing:** Use sample file (e.g., 20260204) to confirm:
- Common Equity rows map to `common_stock` and `primaryExchangeInstrument`
- ETF row maps to `common_stock` and `primaryExchangeInstrument`
- Short positions remain negative via TD quantity
- Fund value equals TD Long MV + TD Short MV sum
- Report date parses from Date column
- FX rate for USD resolves to 1.0

### Themes
- Consistent IDM mapping patterns (reuse exchange treatment instruction and identifier priority)

## Documentation / Knowledge Transfer
Documented mapping rationale, unmapped fields, and future considerations (options/bonds/futures/cash).

## Time Spent
Not tracked (time not referenced).

## Ratings
- **Knowledge / Fluency:** 5
- **My Ability to Service Clearly:** 5
- **Team Ability to Service Clearly:** 5

## Growth Outcome
TBD

## Retrospective
**What went differently than planned?**
TBD

**Key learnings or gotchas:**
- Asked/validated fund value SUM logic in ParserExternalAppUtils (two source columns; no extra functionality needed).
- Production→staging synchronization occurs at 9PM daily; changes made after this time won't be available in staging until the next day's sync.




