# IN-3595 - Eminence Position Size: Portfolio Date Custom Field

**Type:** Bug | Feature | **Enhancement** | Other
**Est:** 1h | **Confidence:** 90%
Completed: [ ]

## Problem & Goal
Add custom field mapping to recently deployed Eminence Position Size adapter (IN-3591) to capture the "businessdate" from column G and map it to "Portfolio Date l Core File" custom field.

Eminence is implementing different businessdate fields across multiple files to support different portfolio views, requiring specific date field naming conventions.

## Deliverables
- Enhanced Eminence Position Size adapter with new custom field mapping
- Column G "businessdate" mapped to "Portfolio Date l Core File" custom field
- Staging validation of new field mapping
- Production deployment of enhanced adapter
- Verification that date appears correctly in Alpha Theory interface

## Entry Points
*Key components from recently deployed adapter*
- **Base Adapter:** Eminence Position Size (IN-3591) - deployed earlier this week
- **External App Settings ID:** 756 (from IN-3591 configuration)
- **External Fund Mapping ID:** 3338
- **Department ID:** 945
- **Fund ID:** 2174
- **Source File:** eminence_position_size (Portfolio_Exposures_YYYYMMDD_YYYYMMDD.csv)
- **Column to Map:** Column G "businessdate"
- **Target Custom Field:** "Portfolio Date l Core File"

## Plan
*High-level approach - bullet points preferred*
- Access existing Eminence Position Size adapter configuration
- Add new custom field mapping for "Portfolio Date l Core File"
- Map column G "businessdate" to the new custom field
- Test mapping in staging environment
- Validate that date field appears correctly in portfolio views
- Deploy enhanced adapter to production
- Confirm successful field population with Eminence data

---

## Execution Notes
*Fill as you work - blockers, discoveries, pivots*

**Context from Jorge's Request:**
Eminence is implementing different "businessdate" fields across multiple files to support various portfolio views. The specific naming "l Core File" distinguishes this date field from other businessdate fields that will be added to other Eminence files.

This enhancement builds directly on the recently deployed Position Size adapter (IN-3591) that was successfully released earlier this week.

### Themes

Client requests for incremental enhancements to recently deployed adapters demonstrate the value of the modern adapter architecture, allowing for quick modifications without full re-implementation.

## Time Spent
**Actual:** [X]h (Research: [X]h | Implementation: [X]h)

## Retrospective
**What went differently than planned?**

**Key learnings or gotchas:**