# IN-3614 - Snoboll Positions File (Cont)

**Type:** Bug | **Feature** | Exploration | Other  
**Est:** 1h | **Confidence:** 70%  
Completed: [y]

## Problem & Goal
Continue IN-3614 work by validating missing CWH option behavior, coordinating handoff, and finalizing delivery paths so Snoboll positions flow into production reliably.

## Deliverables
- Staging and production validation for the missing CWH option
- Snoboll SFTP destination configured and tested
- Email-based delivery path confirmed and build-properties deployed
- Clear next-step ownership for the unresolved CWH visibility issue

## Entry Points
- **Adapter/Issue Context:** Prior week IN-3614 notes (2026-01-26)
- **Staging Validation:** Verify CWH option visibility in the application
- **Delivery Pipeline:** SFTP destination + build-properties deployment + test files
- **Database Check:** Query vwHolisticDepartmentView for Snoboll assets

## Plan
- Review staging output for CWH option visibility with Dan
- Confirm delivery decision with Integration/CX and set up SFTP/email routing
- Deploy build-properties and run delivery tests
- Validate production behavior; log the CWH visibility gap for a follow-on issue

---

## Execution Notes

**Handoff + Staging Review (Sunday/Monday):**
- Dan took over the adapter after a missed execution detail.
- Dan sent for John Ryan review Monday; John could not see the CWH (Camping World) option in the application.
- Dan and I checked staging (~20 min); the option appeared in staging as expected.

**Delivery Path Decision (Tuesday):**
- Integration/CX discussion confirmed Snoboll will send positions via email instead of the adapter file drop.
- Set up Snoboll SFTP destination (~10 min).
- Antoine created the email routing for the positions file.
- Deployed `build-properties` to production and tested delivery (~20 min).

**Production Validation + Follow-up:**
- John suspected the missing CWH option might be a staging bug and requested production deploy.
- Adapter deployed to production; verified CWH still missing in app (~5 min).
- Logged that CWH visibility needs a follow-on issue; DB did not show anomalies.

```sql
select ticker$name,
       ticker$tickerId,
       fundasset$statusID,
       asset$fixedAssetPrice,
       fundAsset$modified,
       fundAsset$fundID,
       fathSummary$sum_shares,
       asset$securityTypeId,
       *
from vwHolisticDepartmentView v
WHERE department$name like '%snoboll%'
order by v.fundAsset$modified desc;
```

### Themes
- **Environment Mismatch Risk:** CWH visibility differed between staging and production, indicating possible environment-specific behavior or UI filtering.

## Time Spent
**Actual:** 0.9h (Research: 0.4h | Implementation: 0.5h)

## Retrospective
**What went differently than planned?**
The delivery path pivoted to email/SFTP, and CWH remained missing even after a production deploy, so the visibility issue was deferred to a new ticket.

**Key learnings or gotchas:**
- Staging results can be misleading for UI visibility; confirm in production before closing.
- Delivery pipeline shifts (email vs file drop) can change the critical path more than adapter changes.
