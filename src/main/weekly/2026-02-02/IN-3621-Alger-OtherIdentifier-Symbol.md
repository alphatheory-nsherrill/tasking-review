# IN-3621 - Alger OtherIdentifier Symbol

**Type:** Bug | Feature | **Exploration** | Other  
**Est:** [X]h | **Confidence:** [X]%  
Completed: [y]

## What / Why / For Whom / How
- **What:** Update Alger positions adapter to use `SYMBOL` (not `NAME`) for OTC `otherIdentifier`.
- **Why:** Ensure correct symbology for private holdings while keeping public equity unchanged.
- **For Whom:** Alger stakeholders and review/approval (John Ryan).
- **How:** Change source column, rerun staging with before/after snapshots, and validate new FundAsset creation.

## Deliverables
- OTC `otherIdentifier` source updated to `SYMBOL`
- Staging run comparison (before/after snapshots)
- Validation that only private holdings changed

## Entry Points
- **Adapter Code:** Alger positions adapter (OTC `otherIdentifier` mapping)
- **Staging Validation:** Snapshot + comparison approach for new FundAssets
- **Review:** John Ryan signoff on staging results

## Plan
- Process the same file with old code and capture a before snapshot
- Process the same file with new code and capture an after snapshot
- Compare created FundAssets and validate expected changes only
- Confirm with reviewer and prepare for release

---

## Execution Notes

**Change + Staging Runs:**
- Updated `otherIdentifier` source to `SYMBOL` for OTC assets (single security type impacted).
- Coordinated staging run sequence using before/after snapshots on the same file.

**Validation + Review:**
- Compared new FundAssets created after the change.
- Reviewer confirmed changes limited to private, non-public equities and no unexpected drops.

## Validation / Execution
- Ran staging with old code, captured snapshot.
- Ran staging with new code, captured snapshot.
- Compared FundAssets created after the change and confirmed with reviewer.

```sql
select fundasset$created as created, fund$fundID as fundId, ticker$name as tickerName, ticker$securityTypeID, *
from vwHolisticDepartmentView
where fund$fundID in (select fundID
                      from ExternalFundMapping
                      where mappingactive = 1
                        and externalappsettingsID in (606, 638, 607))
  and fundasset$statusID = 1
  and fundasset$created > '2026-02-03 15:30'
order by vwHolisticDepartmentView.fundasset$created desc;
```

### Themes
- **Snapshot-Compare Validation:** Using before/after snapshots avoided ambiguity in attribute sourcing.

## Documentation / Knowledge Transfer
- Shared validation results and expectation alignment with reviewer.

## Time Spent
**Actual:** [X]h (Research: [X]h | Implementation: [X]h)

## Ratings
- **Knowledge / Fluency:** [5]
- **My Ability to Service Clearly:** [5]
- **Team Ability to Service Clearly:** [5]

## Growth Outcome
Used this change to understand OTC `otherIdentifier` context and its impact on symbology across private holdings.

## Retrospective
**What went differently than planned?**

**Key learnings or gotchas:**
