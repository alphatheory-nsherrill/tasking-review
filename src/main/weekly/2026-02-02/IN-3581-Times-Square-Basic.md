# IN-3581 - Times Square Basic

**Type:** Bug | Feature | Exploration | **Other**  
**Est:** 3h | **Confidence:** 70%  
Completed: [ ]

## Problem & Goal
Reduce Times Square enrichment runtime by tightening exclusion rules, then validate that scenario/custom-field updates are applied correctly while awaiting final approval.

## Deliverables
- Exclusion logic to skip non-asset header rows and empty scenario/custom-field rows
- Runtime improvement verified in staging
- Scenario update behavior understood and validated with controlled DB changes
- Mapping fix for High Sensitivity applied in staging
- Final signoff pending from John

## Entry Points
- **Prior Context:** 2026-01-26 IN-3581 follow-up notes (performance + FIFO changes)
- **Adapter Runtime:** Times Square enrichment file and skip rules
- **Scenario Updates:** ASSETSCENARIO + CustomFieldInstance validation
- **Review Partner:** John Ryan signoff on staging results

## Plan
- Implement exclusion rules to skip non-asset and empty data rows
- Validate runtime improvement in staging
- Verify scenario updates via SQL and adjust for any mapping mismatches
- Coordinate review with John and await final approval

---

## Execution Notes

**Runtime Focus (Monday):**
- Agreed to emphasize exclusion rules due to 40-minute runtime.
- Implemented InvalidDob skip logic (~1h) when:
  - Identifier is blank, or
  - All scenario/custom-field columns are blank.
- Runtime reduced to ~6 minutes.

**Scenario Validation (Tuesday):**
- Review showed only a few scenarios updated despite more changes in the source (~2h).
- Determined unchanged scenarios are not updated if DB values already match.

```sql
select distinct ticker$bloombergTicker,
                ascen.*
from ASSETSCENARIO ascen
         join vwHolisticDepartmentViewTrim fas on fas.asset$assetID = ascen.assetID
where fas.fund$fundID in (select fundID from EXTERNALFUNDMAPPING where externalAppSettingsID = 755)
  and ticker$bloombergTicker like '%eme%'
order by ascen.modified desc;
```

**Targeted Test + Mapping Fix (Wednesday/Thursday):**
- Coordinated with John for testing; he updated scenarios/custom fields in DB to force visible changes.
- Found mapping typo for "High Sensitivity" (STRL/HOOD) and fixed in staging (~15m).
- Still waiting on John's final signoff.

```sql
select v.ticker$name,
       cf.name,
       cfi.value,
       *
from CUSTOMFIELDINSTANCE cfi
         inner join CustomField cf
                    on cfi.customFieldID = cf.customFieldID
         join vwHolisticDepartmentView v on v.asset$assetID = cfi.assetID
where v.asset$assetID in (select assetID
                          from FUNDASSET
                          where fundID in (select fundID
                                           from ExternalFundMapping
                                           where externalAppSettingsID = 755))
and v.ticker$name in ('HOOD', 'STRL')
```

### Themes
- **Data Skew Drives Runtime:** Non-asset/header and empty rows dominated processing time.
- **Validation Requires Delta Data:** Scenario updates only surface when DB values actually change.

## Time Spent
**Actual:** 3.25h (Research: 2h | Implementation: 1.25h)

## Retrospective
**What went differently than planned?**
Runtime fixes landed quickly, but validation required DB edits to surface changes, and final approval is still pending.

**Key learnings or gotchas:**
- Exclusion rules are the primary lever for performance on sparse files.
- Scenario updates can appear "missing" when data is unchanged; test with forced deltas.
