# IN-3614 - Snoboll Hurricane Positions File

**Type:** Bug | **Feature** | Exploration | Other
**Est:** 4h | **Confidence:** 75%
Completed: [ ]

## Problem & Goal
Implement a new Snoboll Hurricane positions adapter for a file that lacks Bloomberg tickers and explicit security types. Determine security type logic, support new option description format, and validate staging results.

## Deliverables
- Security type rules for the positions file (no Bloomberg ticker, no explicit security type)
- Option parsing for the new "security description" format
- Adapter implementation with instruction container and supporting classes
- Staging run and validation
- Investigation of missing assets or new columns

## Entry Points
*Where to start - key files/docs/concepts to understand first*
- **Source File:** Initial Snoboll Hurricane positions file from IN-3614
- **Security Type Logic:** Derived from available columns and descriptions
- **Options Format:** New pattern in the "security description" column

## Plan
*High-level approach - bullet points preferred*
- Analyze file for security type indicators and option description patterns
- Define security type rules and option regex
- Implement adapter with instruction container and supporting classes
- Run in staging and validate results
- Investigate missing assets and any newly added columns

---

## Execution Notes
*Fill as you work - blockers, discoveries, pivots*

**Initial Analysis:**
- **File Gap:** No Bloomberg ticker and no explicit security type in the source file
- **Security Type Research:** Built a more complex decision tree than needed (1.5h), then simplified to four types:
  - Common Stock
  - Options
  - Equity Swap
  - Index Swap
- **Implementation Estimate:** Expected ~4h to implement after research

**Options Parsing:**
- **New Format:** Options denoted in "security description" with a new pattern
- **Work Done:** Determined regex manually and added a new option type (3h)

**Adapter Work:**
- **Implementation:** Instruction container and supporting classes online in ~2h
- **Staging:** Ran adapter in staging

**Follow-up & Investigation:**
- **Issue Reported:** John Ryan noted missing assets and new columns added to the file
- **Friday Investigation:** Spent 1.5h checking logic and database; no root cause found by EOD Friday

### Themes

**Upfront Research vs. Implementation:** The initial logic exploration was more complex than the final solution, but it clarified the four security types and reduced downstream ambiguity.

**File Volatility:** Late column additions can invalidate assumptions and create missing-asset reports even when parsing logic appears correct.

## Time Spent
**Actual:** 8h (Research: 1.5h | Regex: 3h | Implementation: 2h | Investigation: 1.5h)

## Retrospective
**What went differently than planned?**
The security type logic ended up simpler than expected, but the new option description format required a longer, manual regex effort. The late file changes introduced a missing-assets report that could not be resolved by EOD Friday.

**Key learnings or gotchas:**
- Lack of explicit identifiers (ticker/security type) increases upfront analysis time
- New option description formats can dominate effort if regex is not standardized
- Late file changes can invalidate previous validation assumptions
