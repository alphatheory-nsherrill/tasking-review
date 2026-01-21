# Iridian SFTP Connection Troubleshooting

**Type:** **Bug** | Feature | Exploration | Other
**Est:** 2h | **Confidence:** 60%
Completed: [ ]

## Problem & Goal
Investigate and resolve SFTP connection issues for Iridian NAV files. New credentials provided by client are not working, while existing "old nav way" connection method still functions.

Jorge needs to verify if we're receiving daily NAV files from Iridian and determine if files contain data for single or multiple funds before creating adapter mapping.

## Deliverables
- Successful SFTP connection using new Iridian credentials
- Verification of NAV file reception and frequency
- Analysis of file structure (single vs multiple funds)
- Documentation of connection parameters and troubleshooting steps
- Resolution of authentication or IP allowlisting issues

## Entry Points
*Key components and credentials to investigate*
- **New Credentials Provided:**
  - Hostname: sftp.navbackoffice.com
  - Username: AlphaTheory_Iridian
  - Port: 22
  - Password: [provided in Jorge's email]
- **Current Working Method:** "Old nav way" connection still functional
- **Configuration Files:** build.properties, run-adapter.sh
- **Network Requirements:** IP allowlisting verification needed
- **Client Contact:** Iridian position files uploaded 01/14/2026

## Plan
*Troubleshooting approach - bullet points preferred*
- Test new SFTP credentials using same method as existing Barna connection
- Compare new credential parameters against working "old nav way" configuration
- Investigate build.properties for existing sftp.navbackoffice.com entries
- Verify IP allowlisting status with current network configuration
- Confirm password accuracy and any special character encoding issues
- Test alternative connection methods if primary approach fails
- Document successful connection parameters for future reference
- Analyze received NAV files to determine fund structure for adapter design

---

## Execution Notes
*Fill as you work - blockers, discoveries, pivots*

**Initial Testing Results:**
- New credentials (sftp.navbackoffice.com, AlphaTheory_Iridian, Port 22) fail to connect
- Existing "old nav way" connection method continues to work successfully
- Error suggests authentication failure rather than network connectivity issue

**Investigation with Antoine:**
- Antoine recommended checking build.properties for existing sftp.navbackoffice.com configurations
- Suggested testing other existing credentials to confirm they work
- Need to verify correct password usage and IP allowlisting status
- run-adapter.sh configuration may provide insights into working connection methods

**Current Status:**
- Connection failure isolated to new credential set
- Need follow-up investigation with Antoine to compare against working configurations
- Client waiting for confirmation of NAV file reception capability

### Themes

SFTP connection troubleshooting requires systematic comparison between working and non-working configurations. Client credential changes may involve network allowlisting updates or authentication method modifications that aren't immediately apparent.

## Time Spent
**Actual:** 1.5h (Research: 1.5h | Implementation: [X]h)

## Retrospective
**What went differently than planned?**

**Key learnings or gotchas:**