# Tasking Review Workflow Documentation

This document outlines the complete workflow for creating individual task documents and weekly learning-focused aggregates within the tasking-review system.

## Project Structure

```
src/main/
├── template/
│   ├── TaskingReviewTemplate-Improved.md          # Individual task template
│   └── TaskingReviewAggregateCandidate.md         # Weekly aggregate template
└── weekly/
    └── YYYY-MM-DD/                                # Date-based organization
        ├── [Task-Name].md                         # Individual task documents
        └── weekly-update/
            ├── YYYY-MM-DD-Tasking-Review-Aggregate.md  # Detailed weekly summary
            └── YYYY-MM-DD-Email-Summary.md             # Concise email version
```

## Individual Task Document Workflow

### 1. Task Creation

**Template Usage:**
- Copy `TaskingReviewTemplate-Improved.md` to appropriate weekly folder
- Name files descriptively: `Task-Name.md` or `TICKET-ID-Task-Name.md`
- Include Jira ticket IDs in titles when available: `# IN-3588 - Task Description`

**Required Initial Fields:**
```markdown
**Type:** Bug | Feature | Exploration | Other
**Est:** [X]h | **Confidence:** [X]%
```

### 2. Planning Phase Completion

Fill out before starting work:
- **What / Why / For Whom / How**: One-sentence framing for the task and approach
- **Deliverables**: Concrete outputs expected (code, documents, analysis)
- **Entry Points**: Where to start - key files, docs, concepts
- **Plan**: High-level approach using bullet points (preferred format)

### 3. Execution Tracking

**Real-time Updates:**
- Update "Execution Notes" section as work progresses
- Document blockers, discoveries, and pivots immediately
- Add themes and patterns as they emerge
- Capture validation/execution steps (tests, staging, review, approvals)
- Note documentation/knowledge transfer or close-the-loop actions

**Time Tracking Guidance:**
- Only include time spent when it is explicitly mentioned in the issue or is otherwise essential to the narrative
- If included, use the format: `**Actual:** Xh (Research: Yh | Implementation: Zh)`

### 4. Completion Requirements

**Must Complete:**
- **Validation / Execution**: How the work was confirmed
- **Ratings**: Knowledge/fluency + ability to service (self + team)
- **Growth Outcome**: How this contributed to learning or capability
- **Retrospective**: What went differently than planned + key learnings
- **Themes**: Recurring patterns (if applicable)
- **Documentation / Knowledge Transfer**: What was shared or captured

**Optional Completion Indicators:**
```markdown
Completed: [y] or [n] or [ ]
```

## Key Specifications for Task Documents

### Time Tracking Standards
- Time tracking is optional and should only be included when it is explicitly referenced by the issue or needed for context
- If included, break down time into Research vs Implementation
- Include partial time when tasks are blocked or in progress
- Example: `**Actual:** 2.5h (Research: 0.5h | Implementation: 2h)`

### Jira Integration
- Include Jira ticket numbers in titles when available
- Format: `# TICKET-ID - Description`
- For weekly status, create links: `https://alphatheory.atlassian.net/browse/TICKET-ID`

### Dependencies Tracking
- Document what blocks or enables each task
- Include in both individual tasks and aggregate summaries
- Examples: "Awaiting CX approval", "Requires Mike coordination"

### Follow-up Items (Optional)
- Document future work spawned by current task
- Helps with next week planning and continuity

## Weekly Aggregate Workflow

### 1. Data Collection

**Required for Accurate Aggregation:**
- Re-read all task documents in the weekly folder
- Identify completion status for each task
- Note any dependencies or blockers
- Pull out themes, learnings, and challenges across tasks

### 2. Aggregate Document Creation

**Template Structure (TaskingReviewAggregateCandidate.md):**

```markdown
# NS Tasking Review Learnings [Week Date Range]

## Week Focus
- **Primary Outcomes**: [1-3 sentences on what changed, improved, or was unlocked]
- **Key Challenges**: [1-3 bullets]
- **Most Useful Learnings**: [1-3 bullets]
- **Stakeholder/Dependency Notes**: [short bullets if relevant]

---

### Task: [Title]
**Type:** Bug | Feature | Exploration | Other
**Completed:** Yes | No

#### Framing
- **What / Why / For Whom / How**: [1-2 sentences]
- **Entry Point**: [one sentence]
- **Deliverables**: [one sentence]
- **Context**: [keep short]

#### Learnings & Challenges
**Dependencies**: [Blocked by/Requires/Enables] (only include if applicable)

- **Current Status**: [one sentence OR "Completed"]
- **Validation / Execution**: [tests, staging, review, data checks, approvals]
- **Challenges**: [1-3 bullets]
- **Learnings**: [1-3 bullets]
- **Themes**: [one sentence] (only include if applicable)
- **Deviations from Plan**: [one sentence] (only include if applicable)
- **Knowledge Transfer / Close-the-Loop**: [docs, handoff, stakeholder update] (optional)
- **Follow-up Items**: [What future work this spawned] (optional)
```

### 3. Aggregate Content Guidelines

**Week Focus Guidance:**
- Highlight outcomes, lessons learned, and friction points
- Note dependencies that influenced decisions or timing

**Task Summaries:**
- One sentence for What/Why/For Whom/How, Entry Point, Deliverables
- Keep "Context" concise
- Focus on challenges, learnings, validation, and knowledge transfer

**Overall Sections:**
- **Recurring Themes**: Patterns across multiple tasks
- **Lessons Learned**: What is now understood better
- **Challenges & Friction**: What slowed work or introduced risk
- **Decisions & Tradeoffs**: Key calls made and why
- **Looking Ahead**: Open loops to close next week
- **Knowledge Transfer / Documentation**: What was documented or should be documented

### 4. Weekly Status Reports

**Format Requirements:**
- Organize by functional area (Adapter, IDM/Infrastructure, etc.)
- Use same date-based structure as aggregate documents
- Focus on business value and impact rather than technical details
- **Time Tracking Exclusion**: Do NOT include time spent information in weekly status reports
  - Time tracking remains important for individual task documents
  - Weekly status should focus on accomplishments and outcomes
  - Detailed time analysis available in full aggregate documents

**Content Structure:**
- **Completed**: Tasks finished during the week with key outcomes
- **In Progress**: Current work status and blockers
- **Upcoming**: Planned work for following week
- Include Jira links where applicable
- Emphasize business impact and client outcomes

### 5. Email Summary Creation

**Structure Requirements:**
1. **Week Breakdown**: Lead with outcomes, learnings, and key challenges
2. **Work Review**: Narrative of accomplishments by business area
3. **Detailed Analysis**: Reference to attached aggregate document

**Email Summary Specifications:**
- Target ~200 words (1/6 length of full aggregate)
- Group related tasks by business value
- Focus on completion status and blockers needing attention
- Include key insights and next week priorities
- End with reference to detailed attachment

## Quality Standards

### Individual Task Documents
- **Completeness**: All sections filled before marking complete
- **Accuracy**: Time tracking matches actual work performed (when used)
- **Clarity**: One-sentence summaries that non-technical stakeholders can understand
- **Actionability**: Clear follow-up items and dependencies

### Aggregate Documents
- **Consistency**: Task summaries match individual document details
- **Learning Focus**: Emphasize challenges, lessons, and validation over technical minutiae
- **Forward-Looking**: Clear connection between current week and future work

### Email Summaries
- **Executive-Friendly**: Numbers first, narrative second, details by reference
- **Actionable**: Highlight items needing stakeholder attention
- **Scannable**: Clear structure for busy readers

## Process Improvements Implemented

### Template Evolution
- **Original**: 49 lines, verbose prompts
- **Improved**: 22 lines (55% shorter), clear structure
- **Enhanced**: Added knowledge/validation focus, ratings, and growth outcomes

### Documentation Funnel Vision
- Individual tasks → Weekly aggregates → Management summaries → Enterprise integration
- Designed for potential company-wide rollout as standardized reporting system
- Built-in feedback loop: aggregation process reveals individual task documentation quality

### Key Learnings Applied
- **Estimation Accuracy**: Track patterns in over/under estimation by task type
- **Client Collaboration**: Document iterative feedback loops and their effectiveness
- **System Architecture Discovery**: Capture learning beyond immediate implementation
- **Process Optimization**: Identify and document what works well for replication

## Usage Notes

### When to Use This System
- Multi-step tasks requiring planning and tracking
- Complex technical work benefiting from structured documentation
- Tasks with client collaboration or approval dependencies
- Work that generates learnings applicable to future tasks

### When NOT to Use This System
- Single, straightforward tasks under 1 hour
- Purely conversational or informational requests
- Trivial tasks with no learning value

### Success Metrics
- **Individual Level**: Clearer understanding, higher fluency, deliberate growth tracking
- **Team Level**: Shared learnings, better handoffs, more predictable service quality
- **Organizational Level**: Trend analysis, process improvement identification, strategic planning support

## Integration Points

### With Jira
- Link task documents to Jira tickets via URLs in weekly status
- Include ticket numbers in task titles for traceability

### With Enterprise Systems (Future)
- Designed for Jira/Confluence integration via MCP
- Structured data suitable for business intelligence dashboards
- Standardized format enables automated trend analysis

### With Development Workflow
- Task documents inform code review context
- Retrospectives feed into process improvements
- Dependencies tracking improves project planning

---

*This workflow has been validated through multiple weeks of implementation and refined based on practical usage patterns and stakeholder feedback.*
