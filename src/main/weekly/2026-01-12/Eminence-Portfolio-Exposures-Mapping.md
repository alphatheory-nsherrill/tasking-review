# IN-3591 | Eminence Portfolio_Exposures File Mapping

**Type:** Bug | **Feature** | Exploration | Other  
**Est:** [X]h | **Confidence:** [X]%

## Problem & Goal
Eminence is sending a new file "Portfolio_Exposures" that should be used to map the position size for all assets using columns I and J, along with additional tag data from various columns.

This requires creating a new adapter that works within the Eminence department to process this Portfolio_Exposures file format and classification data.

## Deliverables
- New Eminence Portfolio_Exposures adapter within the Eminence department
- Position size mapping from columns I (exposuredirection) and J (positionsize)
- Tag mapping implementation for:
  - Market Cap tag: col P (marketcap)
  - GIC Sector tag: col O (gicsector)
  - Country tag: col N (countrydesc)
  - Region tag: col M (eodregion)
  - Industry Detail tag: col L (ECIndustryDetail)
  - Industry Summary tag: col K (ecindustrysummary)
- Working adapter that processes Portfolio_Exposures_YYYYMMDD_YYYYMMDD.csv format

## Entry Points
*Key components and data sources to understand first*
- Sample file: `C:\Users\nsherrill\Downloads\Portfolio_Exposures_20260109_20260109.csv`
- Eminence department structure and existing adapter patterns
- File structure analysis:
  - Column I: exposuredirection (L/S for Long/Short)
  - Column J: positionsize (decimal position size values)
  - Columns K-P: Various classification tags for asset categorization
- OpenAdapter framework for new adapter creation
- Eminence department fund mapping and asset matching requirements

## Plan
*High-level approach - bullet points preferred*
- Analyze Portfolio_Exposures file structure and data patterns
- Create new adapter within Eminence department using OpenAdapter framework
- Implement file reading and parsing for Portfolio_Exposures CSV format
- Build position size logic combining exposuredirection (I) and positionsize (J)
- Create tag mapping definitions for all classification fields:
  - Industry Summary (K): ecindustrysummary
  - Industry Detail (L): ECIndustryDetail
  - Region (M): eodregion
  - Country (N): countrydesc
  - GIC Sector (O): gicsector
  - Market Cap (P): marketcap
- Set up Eminence department fund mapping for new adapter
- Test with sample Portfolio_Exposures file data
- Validate position size calculations and tag assignments
- Ensure adapter handles both long (L) and short (S) exposuredirection values

---

## Execution Notes
*Fill as you work - blockers, discoveries, pivots*

**File Analysis from Portfolio_Exposures_20260109_20260109.csv:**
- File contains 163 positions with Fund ID "Classic"
- Position sizes range from -0.1614937667 (SPY short) to 0.0556031044 (INF.LN long)
- exposuredirection shows "L" for long positions, "S" for short positions
- Rich classification data available: industry categories, geographic regions, market cap tiers
- Some assets have combined/custom entries (e.g., "QTZY (Combined)", Goldman basket products)

**Results of Discussion with Jorge - Eminence Position Size Implementation**

Following our discussion regarding the new eminence "Portfolio_Exposures" file for mapping position size:

**Current State:**
- The existing eminence_positions adapter currently maps position size as a custom field
- The new Portfolio_Exposures file is dedicated to more granular position sizing and tagging

**Issue Identified:**
We cannot extract shares count from the Portfolio_Exposures file. The file provides position size only as a percentage of portfolio, but does not include fund value. Without fund value, we cannot calculate absolute position size or derive shares count.

**Requested Changes:**
To proceed with implementation, we need either:
- Fund value added to the Portfolio_Exposures file, OR
- Derived shares count added to the file

**Proposed Adapter Changes:**
- eminence_positions adapter: Remove the "Position Size" custom field mapping (since this will be handled by the dedicated position size adapter)
- Retire eminence_portfolio_analysis_shares_count adapter: This secondary adapter was created to set shares count to $1 based on long/short positions. With the new dedicated position size adapter, this becomes redundant
- Note: The main portfolio analysis adapter will remain active and unchanged

**Next Steps:**
Awaiting file format enhancement before proceeding with the new eminence_position_size adapter implementation.

### Themes

Eminence has been a client that has asked for quite a few adapters, and we have also needed a few rounds of feedback
with either CX or the client. This new file is such a case where we need to circle back with the client.

## Time Spent
**Actual:** [X]h (Research: [X]h | Implementation: [X]h)

## Retrospective
**What went differently than planned?**

**Key learnings or gotchas:**