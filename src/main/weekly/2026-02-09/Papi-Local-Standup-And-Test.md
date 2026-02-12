# PAPI Local Standup and Test

**Type:** Exploration
**Est:** 1h | **Confidence:** 80%
Completed: [x]

## What / Why / For Whom / How
- **What:** Set up PAPI to run locally for debugging purposes.
- **Why:** Enable full-stack debugging of Excel Connect and PAPI code together, rather than only testing against staging.
- **For Whom:** Development team (Antoine and me) preparing for full-local Excel Connect build.
- **How:** Clone PAPI, download latest Wildfly, configure Docker build, attach remote debugger, and verify with API test.

## Deliverables
Working local PAPI instance with documented setup steps for future reference.

## Entry Points
- PAPI repository (separate clone)
- atdev SFTP for Wildfly download
- Docker configuration in /AssetTool/DockerResources
- IntelliJ remote debugger setup

## Plan
- Clone PAPI to separate repository
- Download latest Wildfly from atdev SFTP
- Configure Docker build with Wildfly
- Set up remote debugging through IntelliJ
- Verify functionality with login API test

---

## Execution Notes
**Monday:** Worked with Antoine to get PAPI running locally as preliminary step for Excel Connect debugging.

**Setup Process:**
1. Cloned PAPI to separate repository
2. Connected to atdev SFTP via FileZilla and downloaded latest Wildfly Zip (Feb 2026)
3. Copied and unzipped Wildfly folder into `/AssetTool/DockerResources` in PAPI project
4. Built Docker image: `docker build --build-arg WILDFLY_FOLDER_NAME="wildfly" -t papi .`
5. Started container: `docker run -it -e DEBUGGER_PORT="8787" -e SENDGRIDAPIKEY=your_api_key -e SENDGRIDAPIKEYID=your_api_key_id -p 9990:9990 -p 8443:8443 -p 8787:8787`
6. PAPI required remote debugger attachment before startup - configured through IntelliJ
7. App successfully started after debugger attachment

## Validation / Execution
**API Test:** Verified functionality using Postman login test:
- `POST https://localhost:8443/services/loginTokenizerService`
- Payload: `{"doLogin": [{"arg0": {"email": "dsmith@alphatheory.com","credentials": "LogMeIn2AT!"}}]}`
- Response: Valid token received, confirming local PAPI is functional

### Themes
Local development environment setup and debugging workflow establishment.

## Documentation / Knowledge Transfer
Documented repeatable setup steps for future PAPI local runs. Process serves as refresher and accessible reference documentation.

## Time Spent
Not tracked (brief session with Antoine).

## Ratings
- **Knowledge / Fluency:** 4 *Refreshed existing knowledge of PAPI local setup*
- **My Ability to Service Clearly:** 5 *Process is now documented and repeatable*
- **Team Ability to Service Clearly:** 5

## Growth Outcome
Refreshed and documented local PAPI setup process, enabling more efficient debugging workflows for Excel Connect integration work.

## Retrospective
**What went differently than planned?**
Process went smoothly as expected - mainly a refresher of existing knowledge.

**Key learnings or gotchas:**
- PAPI requires remote debugger attachment before it will fully start up
- Latest Wildfly (Feb 2026) available on atdev SFTP
- Docker build requires specific WILDFLY_FOLDER_NAME argument