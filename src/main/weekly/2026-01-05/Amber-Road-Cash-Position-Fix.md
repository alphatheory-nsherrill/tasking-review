# IN-3588 - Amber Road: Don't Map Cash Position

**Type:** **Bug** | Feature | Exploration | Other
**Est:** 1h | **Confidence:** 95%  
Completed: [y]
## Problem & Goal
Adjust the adapter's instructions so cash is no longer mapped into the app.

Cash positions were being successfully mapped before, but the client no longer wants cash positions included in the application data.

## Deliverables
- Updated adapter mapping to exclude cash positions
- Cash records marked as invalidDob instead of Cash when parsed
- Production deployment with cash mapping disabled

## Entry Points
*Key components and code to understand first*
- Amber Road adapter mapping definitions
- Current cash position handling logic
- External app settings configuration
- Staging and production deployment process

## Plan
*High-level approach - bullet points preferred*
- Identify current cash mapping logic in Amber Road adapter
- Change mapping definition to mark cash records as invalidDob instead of Cash
- Test changes in staging environment
- Get approval for production release
- Deploy to production (coordinate with Antoine for permissions)

---

## Execution Notes
*Fill as you work - blockers, discoveries, pivots*

Made the change in the adapter, and ran it in staging. The whole thing took an hour. Then, with Jorge's approval, Antoine released the code to production.

This was a quick adapter maintenance task, and extremely straightforward. I just changed the mapping definition to say the record is invalidDob instead of Cash when parsed.

**Production Deployment Issue**: I do not have DELETE permissions in production, so I had to ask Antoine to clear the external app settings for me before running. I could have manually updated the fields myself though.

### Themes

**Recurring Issue**: Ongoing problem that I do not have DELETE permissions in production, requiring coordination with Antoine for external app settings cleanup.

**Quick Maintenance**: This was an extremely straightforward adapter configuration change - just updating mapping logic.

## Time Spent
**Actual:** 1.2h (Research: 0.3h | Implementation: 0.9h)

## Retrospective
**What went differently than planned?**

Went exactly to plan - quick and straightforward change.

**Key learnings or gotchas:**

Need to remember to coordinate with Antoine for production permissions when external app settings need clearing. Could potentially handle field updates manually in future similar situations.