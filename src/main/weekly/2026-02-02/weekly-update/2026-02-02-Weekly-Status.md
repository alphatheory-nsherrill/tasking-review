# 2026-02-02

## Completed

### Adapter
* https://alphatheory.atlassian.net/browse/IN-3614 - Snoboll Positions File (Continuation)
  * Confirmed email delivery path and SFTP destination; build-properties deployed
  * Validated CWH option visibility in production (RAPI + app)
* https://alphatheory.atlassian.net/browse/IN-3621 - Alger OtherIdentifier Symbol
  * Switched OTC otherIdentifier to SYMBOL; before/after snapshot validation
  * Confirmed only private holdings affected
* https://alphatheory.atlassian.net/browse/IN-3622 - Gator PFD Assets
  * Moved PFD handling to primary exchange instruments and added FIGI resolution paths
  * Released to production; verified resolved ticker format

## In Progress

### Adapter
* https://alphatheory.atlassian.net/browse/IN-3581 - Times Square Basic
  * Added exclusion rules to cut runtime to ~6 minutes
  * Fixed High Sensitivity mapping in staging
  * John just signed off, so we're good to release to production
  * Waiting to arrange file delivery
* https://alphatheory.atlassian.net/browse/IN-3628 - SOLAS Delisted Security
  * Added zero-price invalidation in parser as interim fix
  * Continued investigation of delisted/ticker drift behavior

## Upcoming

### Adapter
* https://alphatheory.atlassian.net/browse/IN-3625 - Sieve Positions Adapter
* Confirm auto-forwarding rule for Snoboll position file email

### Infrastructure
* Stand up PAPI to run Excel Connect locally
