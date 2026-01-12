# Eminence Price Target Adapter Enhancement

**Type:** Bug | **Feature** | Exploration | Other  
**Est:** 2h | **Confidence:** 90%

## Problem & Goal
The adapter should be enhanced to automatically set and upload price targets for Eminence, utilizing data from the "Eminence Positions" file.

This automation will streamline the price target management process for Eminence positions, reducing manual work and ensuring consistent probability weighting across scenarios.

## Deliverables
Enhanced adapter that:
- Reads price and IRR data from "Eminence Positions" file
- Creates two price targets (PTs) based on IRR scenarios with probability distribution
- Uploads the created price targets to the system
- Process is automated and repeatable

## Entry Points
*Key components and data sources to understand first*
- `EminencePositionsExternalAppInstructionsContainer.java` - current implementation (src/com/wazollc/alphatheory/parser/instructionscontainers/)
- Current data fields already being processed:
  - `CurrentPrice` (line 102, 116) - mapped to "Price" custom field
  - `PricePctBase` (line 75-78) - mapped to "Base" custom field
  - `PricePctDown` (line 85-88) - mapped to "Down" custom field
- `ExternalAppScenariosDefinition` API - currently null (line 55) but needed for price targets
- Price target calculation methodology using CurrentPrice × IRR percentages

## Plan
*High-level approach - bullet points preferred*
**- **Initialize ExternalAppScenariosDefinition** (currently null at line 55) to enable price target functionality
- **Add scenario definitions** for Base IRR scenario (70% probability) and Down IRR scenario (30% probability)
- **Create price target calculation logic using Jorge's formula**:
  - **Formula**: Price Target = Current Price × (1 + IRR)
  - Base Price Target = CurrentPrice × (1 + PricePctBase)
  - Down Price Target = CurrentPrice × (1 + PricePctDown)
  - **Note**: IRR values are already in decimal format (e.g., 1.701385532), not percentages
- **Configure scenario mappings** to connect existing data fields to price target scenarios
- **Test with existing data fields** (CurrentPrice, PricePctBase, PricePctDown already being processed)
- **Validate price target creation** in the adapter output
- **Verify 70/30 probability weighting** is correctly applied to the scenarios
- **Test end-to-end workflow** with sample Eminence Positions file data**

---

## Execution Notes
*Fill as you work - blockers, discoveries, pivots*

**Code Analysis Findings:**
- EminencePositionsExternalAppInstructionsContainer already processes all required data fields (CurrentPrice, PricePctBase, PricePctDown)
- The infrastructure for custom fields and numeric processing is in place
- Key missing piece: ExternalAppScenariosDefinition implementation (line 55 currently null)
- Price target calculation will use existing numeric processing pipeline with adjustment factors

**Formula Clarification (from Jorge):**
- Confirmed formula: **Price Target = Current Price × (1 + IRR)**
- IRR values are already in decimal format (e.g., 1.701385532), not percentages
- Example: 37.53 × (1 + 1.701) = 101.36853
- No division by 100 needed - PricePctBase and PricePctDown are ready to use as-is

Finished on Friday, deployed to staging. Will need to follow up Monday for approval from CX

### Themes

Explicit clarification in Jira on requirements before beginning work

## Time Spent
**Actual:** 2.5h (Research: .2h | Implementation: 2.3h)

## Retrospective
**What went differently than planned?**

Went to plan

**Key learnings or gotchas:**

Ran into issue on Friday where I deployed the code to staging Thursday night, but an automated script deployed the base
staging branch back on top of it overnight. Added 20 minutes of debugging, only to just redeploy the branch and have
the code work.

Main learning was implementing scenarios on my own - how to assign intermediate fields to explicit scenario names and
construct the Explicit Scenaio Names map

---

## Acceptance Criteria
- [ ] Adapter can read Eminence Positions file
- [ ] Price targets are calculated from Base and Down IRRs
- [ ] Two PTs are created per position with correct probabilities (70/30)
- [ ] Price targets are successfully uploaded to the system
- [ ] Process is automated and repeatable