# IN-3628 - SOLAS Delisted Security

**Type:** Bug | Feature | **Exploration** | Other  
**Est:** [X]h | **Confidence:** [X]%  
Completed: [ ]

## What / Why / For Whom / How
- **What:** Investigate a SOLAS delisted/security identifier change causing unexpected symbology results; provide an intermediate fix to help Dan.
- **Why:** Prevent incorrect ticker resolution and downstream pricing/position issues.
- **For Whom:** SOLAS stakeholders and internal data/adapter teams.
- **How:** Trace symbology history, inspect raw source rows, and apply validation logic in the parser.

## Deliverables
- Initial analysis of the ticker change behavior (intermediate step)
- Validation logic to flag zero-priced assets as invalid
- Staging verification of the change

## Entry Points
- **Symbology Tables:** `portfolioMapping.source.symbologyData`, `portfolioMapping.source.ExposuresData`
- **Raw Source Rows:** `portfolioMapping.source.RawSourceRow`
- **Resolution View:** `portfolioMapping.mapped.SymbologyResolvedTicker`
- **Adapter Logic:** `AdapterHedgeServSolasParser`

## Plan
- Query symbology and exposure records around the ticker change window
- Confirm how the raw rows are resolving and whether delisting logic exists
- Add validation to prevent zero-priced assets from being treated as valid
- Re-run in staging and review with Dan

---

## Execution Notes

**Investigation:**
- Observed a ticker change that was not caught; reviewed symbology history and raw rows.
- Verified resolution behavior for the affected symbology hash codes.

```sql
select * from portfolioMapping.source.symbologyData
where externalAppSettingsId = 384
  and created > '2026-01-18'
  and bloombergTicker in ('LOGC US EQUITY', 'LOGCD US EQUITY');

select * from portfolioMapping.source.ExposuresData
where created > '2026-01-18'
  and symbologyHashCode in (-827578365, 97364125, -663175698);

select * from portfolioMapping.source.RawSourceRow
where created > '2026-01-25'
  and symbologyHashCode in (-827578365, 97364125, -663175698);

select * from portfolioMapping.mapped.SymbologyResolvedTicker
where symbologyHashCode = -663175698;
```

**Intermediate Fix (to help Dan):**
- Added validation in `AdapterHedgeServSolasParser` to mark assets invalid when calculated `localPrice = 0`.
- Walked through the updated logic in staging with Dan; fix is a starting point and not fully resolved yet.

## Validation / Execution
- Staging logic walkthrough with Dan after introducing zero-price invalidation.

### Themes
- **Delisted/Ticker Drift:** Symbology changes can bypass expected checks if delisting signals aren’t explicit.

## Documentation / Knowledge Transfer
- Discussed approach and parser changes with Dan during walkthrough.

## Time Spent
**Actual:** [X]h (Research: [X]h | Implementation: [X]h)

## Ratings
- **Knowledge / Fluency:** [1]
- **My Ability to Service Clearly:** [3]
- **Team Ability to Service Clearly:** [3]

## Growth Outcome
*How does this contribute to my growth or the team's shared knowledge?*

Will watch solution as Dan develops it

## Retrospective
**What went differently than planned?**

**Key learnings or gotchas:**
- Legacy adapter behavior requires careful tracing of symbology and pricing flow.
