# Iridian SFTP Connection Troubleshooting

**Type:** **Bug** | Feature | Exploration | Other
**Est:** 2h | **Confidence:** 60%
Completed: [y]

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

**Email Chain Analysis & IP Discovery:**
- Jorge provided raw email chain from Iridian credential setup
- Attempted login again using new credentials with same failure result
- Reading through email chain revealed potential IP allowlisting issue
- Discovered that only public IP addresses are allowed for SFTP access
- Current connection attempts are coming from s-adapter which may not be on allowlist
- Requested Jorge reach out to Iridian to get Alpha Theory emails/IPs whitelisted

**SFTP Connection Resolution:**
- Iridian updated their IP allowlist to include Alpha Theory access
- Successfully connected to SFTP server using new credentials
- Able to download NAV files from Iridian SFTP server
- Connection issue fully resolved - can now proceed with regular file retrieval

**Current Status:**
- ✅ SFTP connection working successfully
- ✅ File download capability confirmed
- Ready to proceed with NAV file analysis for adapter mapping
- Can begin development of Iridian adapter based on downloaded file structure

### Themes

**Systematic Network Troubleshooting:** This resolution demonstrates the importance of comprehensive troubleshooting approaches that combine technical testing with contextual analysis. When standard credential and configuration testing failed, email chain analysis provided the critical insight that revealed IP allowlisting restrictions not apparent from technical error messages.

SFTP connection troubleshooting requires systematic comparison between working and non-working configurations, but technical approaches must be supplemented with communication context analysis. Client credential changes may involve network allowlisting updates or authentication method modifications that aren't immediately apparent from connection errors.

The progression from technical testing → configuration comparison → email chain analysis → root cause identification establishes a valuable methodology for similar network connectivity issues. IP allowlisting restrictions are common in client SFTP setups and should be investigated early when credentials appear technically correct.

## Time Spent
**Actual:** 2.5h (Research: 2h | Implementation: 0.5h)

## Retrospective
**What went differently than planned?**

Initial focus was on credential and configuration issues, but the root cause turned out to be IP allowlisting restrictions that weren't immediately apparent from the technical error messages. Email chain analysis provided the key insight that led to identifying the actual blocker. Resolution was straightforward once Iridian updated their allowlist.

**Key learnings or gotchas:**

When SFTP credentials fail but appear technically correct, IP allowlisting should be investigated early in the troubleshooting process. Client email chains often contain critical context about network restrictions that aren't obvious from connection error messages. Many clients implement strict IP allowlisting for SFTP access that requires explicit coordination to resolve. Once the IP issue was identified and communicated, client resolution was quick and effective.