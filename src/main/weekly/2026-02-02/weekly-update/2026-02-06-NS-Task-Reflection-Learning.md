# NS Tasking Review Learnings [2026-02-02]

## Week Focus
- **Primary Outcomes**: Reduced adapter runtime, improved ticker resolution paths, and validated delivery/visibility workflows across multiple client feeds.
- **Key Challenges**: Environment mismatches, identifier gaps in resolution paths, and approvals gating final closure.
- **Most Useful Learnings**: Snapshot-based validation, forcing deltas for scenario checks, and tracing symbology resolution through legacy adapters.
- **Stakeholder/Dependency Notes**: Final approval pending for Times Square; SOLAS fix is an intermediate step supporting Dan.

---

### Task: IN-3581 - Times Square Basic

**Type:** Other  
**Completed:** No (awaiting John’s final signoff)

#### Framing
- **What / Why / For Whom / How**: Reduce Times Square enrichment runtime and validate scenario/custom-field updates for stakeholder confidence and correctness.
- **Entry Point**: Enrichment file skip rules + scenario/custom-field checks.
- **Deliverables**: Exclusion logic, mapping fix, and validation evidence.
- **Context**: Prior FIFO follow-up and performance concerns.

#### Learnings & Challenges
**Dependencies**: John Ryan approval

- **Current Status**: Runtime improved; mapping fix applied; approval pending.
- **Validation / Execution**: Staging runtime checks, SQL scenario validation, reviewer-driven DB deltas.
- **Challenges**: Scenario updates only surface with data deltas; approval timing.
- **Learnings**: Exclusion rules are the primary performance lever; validation needs forced deltas.
- **Themes**: Data skew and unchanged values mask progress.
- **Deviations from Plan**: Validation required DB edits to show changes.
- **Knowledge Transfer / Close-the-Loop**: Coordinated testing expectations with John; documented High Sensitivity mapping fix.
- **Follow-up Items**: Await final signoff.

---

### Task: IN-3614 - Snoboll Positions File (Cont)

**Type:** Feature  
**Completed:** Yes

#### Framing
- **What / Why / For Whom / How**: Validate CWH option visibility and finalize delivery paths for Snoboll to ensure reliable production flow.
- **Entry Point**: CWH visibility checks + delivery pipeline (SFTP/email).
- **Deliverables**: Validation results and delivery setup.
- **Context**: Hand-off review and environment discrepancy.

#### Learnings & Challenges
**Dependencies**: Integration/CX delivery decision

- **Current Status**: Delivery path set; CWH visibility resolved after production validation.
- **Validation / Execution**: Staging review, production deploy, DB query, and RAPI response check.
- **Challenges**: Staging vs. production visibility mismatch.
- **Learnings**: Production verification and API response checks close visibility gaps.
- **Themes**: Environment mismatch risk.
- **Deviations from Plan**: Delivery path pivoted from file drop to email/SFTP.
- **Knowledge Transfer / Close-the-Loop**: Shared API request method for RAPI validation.

---

### Task: IN-3621 - Alger OtherIdentifier Symbol

**Type:** Exploration  
**Completed:** Yes

#### Framing
- **What / Why / For Whom / How**: Switch OTC otherIdentifier from `NAME` to `SYMBOL` to maintain correct symbology for private holdings.
- **Entry Point**: OTC otherIdentifier mapping + staging snapshot comparison.
- **Deliverables**: Source column change and validation that only private holdings changed.
- **Context**: Focused, controlled staging validation.

#### Learnings & Challenges
**Dependencies**: Reviewer signoff

- **Current Status**: Change validated and approved.
- **Validation / Execution**: Before/after snapshots on same file; FundAsset comparison.
- **Challenges**: Ensure no unintended drops.
- **Learnings**: Snapshot comparisons eliminate ambiguity in attribute sourcing.
- **Themes**: Controlled validation yields confidence quickly.
- **Knowledge Transfer / Close-the-Loop**: Shared validation results with reviewer.

---

### Task: IN-3622 - Gator PFD Assets

**Type:** Exploration  
**Completed:** Yes

#### Framing
- **What / Why / For Whom / How**: Fix PFD mapping/pricing and ensure FIGI resolution passes Bloomberg identifiers.
- **Entry Point**: PFD handling rules + `TickerResolutionPathProcessor`.
- **Deliverables**: Resolution path updates and production release.
- **Context**: OTC mapping caused pricing mismatch; needed better resolution path coverage.

#### Learnings & Challenges
**Dependencies**: Reviewer coordination

- **Current Status**: Released to production.
- **Validation / Execution**: Resolved ticker format verification in staging.
- **Challenges**: Identifier pass-through gaps in legacy resolution paths.
- **Learnings**: FIGI path completeness is critical for preferred stock handling.
- **Themes**: Missing identifiers silently break matching.
- **Knowledge Transfer / Close-the-Loop**: Shared CIM validation guidance and cleanup of OTC duplicates.

---

### Task: IN-3628 - SOLAS Delisted Security

**Type:** Exploration  
**Completed:** No (intermediate step)

#### Framing
- **What / Why / For Whom / How**: Investigate delisted ticker behavior and add a guardrail to help Dan while root cause is pursued.
- **Entry Point**: Symbology history + raw source rows + parser validation logic.
- **Deliverables**: Intermediate zero-price invalidation and staging walkthrough.
- **Context**: Ticker drift not caught by existing checks.

#### Learnings & Challenges
**Dependencies**: Ongoing fix development with Dan

- **Current Status**: Intermediate fix in place; full resolution pending.
- **Validation / Execution**: Staging walkthrough after adding zero-price invalidation.
- **Challenges**: Delisting signals are indirect; legacy adapter flow is hard to trace.
- **Learnings**: Symbology drift can bypass expected checks; guardrails reduce risk.
- **Themes**: Legacy adapter tracing is slow but necessary.
- **Knowledge Transfer / Close-the-Loop**: Walkthrough and handoff with Dan.
- **Follow-up Items**: Complete full fix and validate delisting logic.

---

## Overall

### Recurring Themes
- Environment and data deltas drive perceived correctness.
- Identifier pass-through gaps are a common failure mode.
- Snapshot-based validation improves confidence and review speed.

### Lessons Learned
- Exclusion rules and data sparsity dominate adapter performance.
- Forcing deltas is necessary when validation is based on change detection.
- Legacy adapter flows require end-to-end tracing to avoid silent mismatches.

### Challenges & Friction
- Approvals and review timing delayed final closure on some tasks.
- Staging vs. production differences obscured true visibility.

### Decisions & Tradeoffs
- Adopted email/SFTP delivery for Snoboll instead of file-drop.
- Applied an intermediate guardrail for SOLAS to reduce risk while the full fix is developed.

### Looking Ahead
- Obtain final signoff for Times Square.
- Complete SOLAS delisted/security resolution and re-validate in staging/production.

### Knowledge Transfer / Documentation
- Documented RAPI validation method and CIM validation guidance.
- Shared mapping fixes and review expectations with stakeholders.
