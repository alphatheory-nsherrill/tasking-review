# Tasking Review Workflow Documentation

This document outlines the complete workflow for creating individual task tracking documents and weekly aggregate summaries within the tasking-review system.

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
- **Problem & Goal**: One-sentence problem statement and objective
- **Deliverables**: Concrete outputs expected (code, documents, analysis)
- **Entry Points**: Where to start - key files, docs, concepts
- **Plan**: High-level approach using bullet points (preferred format)

### 3. Execution Tracking

**Real-time Updates:**
- Update "Execution Notes" section as work progresses
- Document blockers, discoveries, and pivots immediately
- Add themes and patterns as they emerge

**Time Tracking Requirements:**
- Mark tasks as in_progress when starting
- Update actual time spent immediately upon completion
- Format: `**Actual:** Xh (Research: Yh | Implementation: Zh)`
- Track both total and breakdown by activity type

### 4. Completion Requirements

**Must Complete:**
- **Time Spent**: Actual hours with research/implementation breakdown
- **Retrospective**: What went differently than planned + key learnings
- **Themes**: Recurring patterns (if applicable)

**Optional Completion Indicators:**
```markdown
Completed: [y] or [n] or [ ]
```

## Key Specifications for Task Documents

### Time Tracking Standards
- Always track actual vs estimated time
- Break down time into Research vs Implementation
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
- Verify actual time tracking is complete and accurate
- Identify completion status for each task
- Note any dependencies or blockers

### 2. Aggregate Document Creation

**Template Structure (TaskingReviewAggregateCandidate.md):**

```markdown
# NS Tasking Review Aggregation [Week Date Range]

## Week Summary
- **Total Hours**: Xh (Estimated: Yh, Variance: +/-Zh)
- **Task Types**: X bugs, Y features, Z exploration
- **External Dependencies**: X waiting on client, Y waiting on approvals

---

### Task: [Title]
**Type:** Bug | Feature | Exploration | Other
**Completed:** Yes | No

#### Background
- **Problem and/or Goals**: [one sentence]
- **Entry Point**: [one sentence]
- **Deliverables**: [one sentence]
- **Addtl Details**: [keep short]

#### Execution Notes
**Approx. Completion Time: [X]h**
**Dependencies**: [Blocked by/Requires/Enables] (only include if applicable)

- **Current Status**: [one sentence OR "Completed"]
- **Notes Summary**: [keep short]
- **Themes**: [one sentence] (only include if applicable)
- **Deviations from Plan**: [one sentence] (only include if applicable)
- **Learnings**: [keep short]
- **Follow-up Items**: [What future work this spawned] (optional)
```

### 3. Aggregate Content Guidelines

**Week Summary Calculations:**
- Sum all actual hours from individual tasks
- Sum all estimated hours where available
- Calculate variance (actual - estimated)
- Count task types and external dependencies

**Task Summaries:**
- One sentence for Problem/Goals, Entry Point, Deliverables
- Keep "Addtl Details" and "Notes Summary" concise
- Only include Themes/Deviations/Learnings if meaningful
- Focus on business value and learnings over technical details

**Overall Sections:**
- **Recurring Themes**: Patterns across multiple tasks
- **Highlights**: Tasks that moved the needle most
- **Looking Ahead**: Unfinished work for next week
- **Efficiency Gains**: What worked well (processes, tools, approaches)

### 4. Email Summary Creation

**Structure Requirements:**
1. **Week Breakdown**: Lead with hard numbers and metrics
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
- **Accuracy**: Time tracking matches actual work performed
- **Clarity**: One-sentence summaries that non-technical stakeholders can understand
- **Actionability**: Clear follow-up items and dependencies

### Aggregate Documents
- **Mathematical Accuracy**: Time calculations must be verified by re-reading source documents
- **Consistency**: Task summaries match individual document details
- **Business Value Focus**: Emphasize impact and learning over technical complexity
- **Forward-Looking**: Clear connection between current week and future work

### Email Summaries
- **Executive-Friendly**: Numbers first, narrative second, details by reference
- **Actionable**: Highlight items needing stakeholder attention
- **Scannable**: Clear structure for busy readers

## Process Improvements Implemented

### Template Evolution
- **Original**: 49 lines, verbose prompts
- **Improved**: 22 lines (55% shorter), clear structure
- **Enhanced**: Added Dependencies field and Follow-up Items section

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
- **Individual Level**: Improved estimation accuracy, better knowledge retention
- **Team Level**: Consistent documentation format, easier knowledge transfer
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