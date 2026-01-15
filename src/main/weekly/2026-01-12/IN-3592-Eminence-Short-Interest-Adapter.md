# IN-3592 - Eminence: Adapter for Short Interest Report

**Type:** Bug | **Feature** | Exploration | Other
**Est:** [X]h | **Confidence:** [X]%

## Problem & Goal
Create new adapter for Eminence Short Interest Report data mapping, focusing on short interest metrics and retail participation data.

Note: Column names in the issue description are not correct - need to consult the actual file for proper column mapping.

## Deliverables
- New Eminence Short Interest Report adapter
- Custom field mappings with proper data formatting:
  - "Short Interest": markit_si_pct column (multiply by 100 for percentage)
  - "SI Date": markit_asof column
  - "Retail Participation Rank": retail_shares_ma_21d_rnk column (multiply by 100 for percentage)
  - "Retail Date": retail_data_date column
- Working adapter that processes Portfolio_SI_Retail_YYYYMMDD_YYYYMMDD.csv format

## Entry Points
*Key components and data sources to understand first*
- Actual file: `C:\Users\nsherrill\Documents\positionsdev\Portfolio_SI_Retail_20260112_20260112.csv`
- Verified column mappings:
  - markit_si_pct → "Short Interest" custom field
  - markit_asof → "SI Date" custom field
  - retail_shares_ma_21d_rnk → "Retail Participation Rank" custom field
  - retail_data_date → "Retail Date" custom field
- Mapping configuration details:
  - Dept ID: 945
  - Fund ID: 2174
  - External App ID: 492
  - External App Settings ID: 757
  - External Fund Mapping ID: 3339
- OpenAdapter framework for custom field mapping
- Percentage value processing (multiply by 100 for display)

## Plan
*High-level approach - bullet points preferred*
- Create new adapter within Eminence department using provided mapping configuration
- Implement custom field definitions for short interest and retail participation data
- Add percentage processing logic (multiply by 100) for Short Interest and Retail Participation Rank
- Map date fields for SI Date and Retail Date
- Test adapter with sample file data
- Validate custom field creation and percentage formatting
- Ensure proper fund/department mapping configuration

---

## Execution Notes
*Fill as you work - blockers, discoveries, pivots*

**Configuration Details:**
- Dept ID: 945
- Fund ID: 2174
- External App ID: 492
- External App Settings ID: 757
- External Fund Mapping ID: 3339

**Verified Column Mappings from Portfolio_SI_Retail_20260112_20260112.csv:**
- markit_si_pct → "Short Interest" (multiply by 100)
- markit_asof → "SI Date"
- retail_shares_ma_21d_rnk → "Retail Participation Rank" (multiply by 100)
- retail_data_date → "Retail Date"

### Themes

Eminence has been a client that has asked for quite a few adapters, and we have also needed a few rounds of feedback
with either CX or the client.

## Time Spent
**Actual:** [X]h (Research: [X]h | Implementation: [X]h)

## Retrospective
**What went differently than planned?**

**Key learnings or gotchas:**