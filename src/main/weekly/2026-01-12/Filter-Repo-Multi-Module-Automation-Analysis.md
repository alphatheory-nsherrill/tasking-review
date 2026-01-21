# Filter-Repo Multi-Module Automation Analysis

**Type:** Exploration
**Est:** 4h | **Confidence:** 80%
Completed: [ ]

## Problem & Goal
Investigate FILTER_REPO_PROMOTION_GUIDE.md and determine automation approach for extracting multiple IDM patterns: IDM-31 (scoring/pricing), ticker-matching (ATOP/Arcana/RAPI), atomic-adapter, FIGI-exposure, guidepost systems.

## Deliverables
- Analysis of guide's automation strategy
- Recommendations for multi-pattern extraction workflow
- Manifest design for each target pattern
- Version alignment strategy for interdependent patterns

## Entry Points
*Where to start? Key files/docs/concepts to understand first*
- **Primary Reference**: `scripts/FILTER_REPO_PROMOTION_GUIDE.md` - comprehensive extraction process
- **Key Automation Components**:
  - Manifest-driven approach (`manifests/*.yaml`)
  - Extraction scripts (`generate-filter-command.sh`, `extract-domain.sh`)
  - Validation scripts (`validate-extraction.sh`)
- **Target Patterns to Extract**:
  - IDM-31: Scoring and pricing functionality
  - Ticker Systems: ATOP/Arcana/RAPI-request/TickerMatching
  - Adapter Systems: Guidepost → Find or Create Ticker
  - Atomic Adapter: Master→Atomic Adapter
  - FIGI Exposure: Independent FIGI (sits on Atomic Adapter)

## Plan
*Investigation findings and next steps*

**Guide Analysis (COMPLETED):**
- Guide uses 3-phase automation: Analysis → Extraction → Publishing
- Manifest-driven approach with YAML files defining extraction scope
- Validation pipeline: compile → test → dependency analysis

**Key Findings:**
- Pattern interdependencies exist (FIGI sits on Atomic Adapter)
- Need pattern families: Ticker Systems (ticker-matching, atomic-adapter, figi) vs CX Systems (scoring-pricing, guidepost)
- Aligned versioning recommended for interdependent patterns
- Master orchestrator needed for parallel extraction

**Next Steps:**
- Create manifest files for each pattern (scoring-pricing, ticker-matching, atomic-adapter, figi-exposure)
- Build master extraction orchestrator script
- Implement dependency graph analysis
- Design pattern family coordination strategy

---

## Execution Notes
*Investigation phase only - implementation pending*

### Themes

## Time Spent
**Actual:** xh (Research: xh)

## Retrospective
**What went differently than planned?**

Investigation complete, ready for implementation phase.

**Key learnings or gotchas:**

- Pattern interdependencies require dependency graph analysis before extraction
- Aligned versioning simpler than independent versioning for interdependent patterns
- Guide's automation framework maps well to multi-pattern challenges