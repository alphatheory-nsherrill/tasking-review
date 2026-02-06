# IN-3622 - Gator PFD Assets

**Type:** Bug | Feature | **Exploration** | Other  
**Est:** [X]h | **Confidence:** [X]%  
Completed: [y]

## What / Why / For Whom / How
- **What:** Investigate Gator preferred stock (PFD) assets mapping/pricing and fix ticker resolution.
- **Why:** Local Price should drive pricing; current OTC mapping caused mismatches and incorrect resolution.
- **For Whom:** Gator stakeholders and adapter reviewers (Jorge Astorga).
- **How:** Adjust PFD handling and FIGI resolution paths; validate resolved ticker format.

## Deliverables
- Updated PFD handling from OTC to Primary Exchange instruments
- FIGI-mapped PFDs included in ticker resolution paths
- Validation that resolved tickers use Bloomberg format (not `S:`)
- Production release

## Entry Points
- **Adapter Instructions:** Pricing/mapping logic for PFD assets
- **Resolution Flow:** `ATAdapterStations` + `TickerResolutionPathProcessor`
- **Validation Table:** `PortfolioMapping.adapter.StateBeanResolvedTickerDetails`

## Plan
- Review adapter instructions for Local Price mapping
- Adjust PFD handling and resolution path flow
- Validate resolved ticker output format in staging
- Coordinate review and release to production

---

## Execution Notes

**Initial Findings:**
- PFD records lacked traditional FIGI matches; OTC mapping produced mismatched pricing.
- Shifted PFD handling to Primary Exchange instruments to correct naming.

**Resolution Flow Fix:**
- Found Bloomberg identifier was not passed out of `TickerResolutionPathProcessor`.
- Added FIGI-mapped PFDs to the list of FIGI resolution paths and processed them in the resolver.

**Coordination + Release:**
- Shared staging updates with Jorge for review (search for CIM; ignore older OTC copies).
- Released to production Friday evening.

## Validation / Execution
- Verified `resolvedTickerName` uses Bloomberg format (not `S:`) after changes.

```sql
select *
from PortfolioMapping.adapter.StateBeanResolvedTickerDetails
where externalAppHistoryID = (SELECT MAX(externalAppHistoryID)
                              from EXTERNALAPPHISTORY
                              where EXTERNALAPPHISTORY.externalAppSettingsID = 698
                                and type = 'data file capture');
```

### Themes
- **Resolution Path Completeness:** Missing identifier pass-through can silently break matching.

## Documentation / Knowledge Transfer
- Coordinated review notes with Jorge; documented how to validate CIM and ignore older OTC copies.

## Time Spent
**Actual:** [X]h (Research: [X]h | Implementation: [X]h)

## Ratings
- **Knowledge / Fluency:** [3]
- **My Ability to Service Clearly:** [4]
- **Team Ability to Service Clearly:** [5]

## Growth Outcome
*How does this contribute to my growth or the team's shared knowledge?*

This was a hands-on look at the ticker mapping portion of the code - the ability to diagnose a problem was boosted by the encouragement that showed me exactly what I needed to change.

## Retrospective
**What went differently than planned?**

**Key learnings or gotchas:**
- Preferred stock mappings can fail silently when FIGI paths are incomplete.
