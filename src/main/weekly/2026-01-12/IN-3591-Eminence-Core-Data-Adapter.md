# IN-3591 - Eminence: Adapter with "core" data for all assets

**Type:** Bug | **Feature** | Exploration | Other
**Est:** 3h | **Confidence:** 90%

## Problem & Goal
Eminence is sending a new file "Portfolio_Exposures" that should be used to map the position size for all assets using columns I and J, along with additional tag data from various columns.

Eminence has worked with us on this file and added columns R (quantityend), S (exposurebook), T (endingaum), and U (endpricebook), so this is basically a positions file at this point.

## Deliverables
- New Eminence "core data" adapter for Portfolio_Exposures file processing
- Position size mapping from columns I (exposuredirection) and J (positionsize)
- Enhanced position data mapping from new columns:
  - Column R: quantityend
  - Column S: exposurebook
  - Column T: endingaum
  - Column U: endpricebook
- Tag mapping implementation for:
  - Market Cap tag: col P
  - GIC Sector tag: col O
  - Country tag: col N (countrydesc)
  - Region tag: col M (eodregion)
  - Industry Detail tag: col L (ECIndustryDetail)
  - Industry Summary tag: col K (ecindustrysummary)

## Entry Points
*Key components and data sources to understand first*
- Original analysis file: `C:\Users\nsherrill\Downloads\Portfolio_Exposures_20260109_20260109.csv`
- Enhanced file: `C:\Users\nsherrill\Documents\positionsdev\Portfolio_Exposures_20260114_20260114.csv`
- Mapping configuration details:
  - Dept ID: 945
  - Fund ID: 2174
  - External App ID: 492
  - External App Settings ID: 756
  - External Fund Mapping ID: 3338
- Position file structure with new columns R, S, T, U
- Tag mapping columns K-P for asset classification
- OpenAdapter framework for positions file processing
- Current "no positions found" error investigation

## Plan
*High-level approach - bullet points preferred*
- Analyze enhanced Portfolio_Exposures file with new position columns (R, S, T, U)
- Debug "no positions found" error in current adapter implementation
- Review adapter configuration with provided mapping IDs
- Implement position size logic combining exposuredirection (I) and positionsize (J)
- Add enhanced position data mapping for quantityend, exposurebook, endingaum, endpricebook
- Create tag mapping definitions for all classification fields (K through P)
- Test adapter with enhanced positions file format
- Validate position processing and tag assignments
- Ensure proper fund/department mapping configuration

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

**File Enhancement by Eminence:**
- Eminence worked with us on this file and added columns R (quantityend), S (exposurebook), T (endingaum), and U (endpricebook)
- This enhancement made it a full positions file, addressing the shares count calculation issue

**Current Implementation Status:**
- Adapter implementation started but encountering "no positions found" error
- Everything appears configured correctly based on provided mapping details
- File enhanced by Eminence with additional columns R, S, T, U making it a full positions file

**Issue Resolution:**
- "No positions found" warning wasn't an adapter code issue
- Root cause: ExternalFundApproval mapping wasn't created in the database
- Fixed by creating the ExternalFundApproval mapping myself - adapter now runs successfully

**Configuration Details:**
- Dept ID: 945
- Fund ID: 2174
- External App ID: 492
- External App Settings ID: 756
- External Fund Mapping ID: 3338

### Themes

Eminence has been a client that has asked for quite a few adapters, and we have also needed a few rounds of feedback with either CX or the client. This new file is such a case where we need to circle back with the client.

The evolution from initial file analysis → Jorge discussion about missing data → client file enhancement → implementation → database configuration issue demonstrates the iterative nature of complex adapter development.

## Time Spent
**Actual:** [X]h (Research: 1.5h | Implementation: [X]h)

## Retrospective
**What went differently than planned?**

**Key learnings or gotchas:**