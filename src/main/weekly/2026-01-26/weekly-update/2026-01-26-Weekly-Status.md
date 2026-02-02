# 2026-01-26

## Completed

### Adapter
* https://alphatheory.atlassian.net/browse/IN-3597 - Eminence Alpha View Adapter Implementation
  * Implemented full adapter with required field mappings and percentage handling
  * Staging setup required new external app settings and fund mapping
  * Review clarified "run date" as a custom field for simpler implementation
  * Released and validated in production

## In Progress

### Adapter
* https://alphatheory.atlassian.net/browse/IN-3581 - FIFO Matching System Follow-up (Continuation)
  * Verification targets changed; FIFO removed after requirements shift
  * Optimized staging runtime from 40 minutes to 6 minutes by skipping unproductive rows
  * Waiting on confirmed file delivery channel (ad hoc email vs. SFTP)
* **Finepoint Enhanced Adapter - Deployment & Refinements (Continuation)**
  * 12 hours of additional security-type verification due to complexity
  * Initial report revised after feedback; pivoted to a more direct identifying column
  * Handoff to Antoine to close out with Dan; final decisions captured on video
* https://alphatheory.atlassian.net/browse/IN-3614 - Snoboll Hurricane Positions File
  * Security type logic narrowed to Common Stock, Options, Equity Swap, Index Swap
  * New options regex implemented for "security description" format
  * Adapter implemented and run in staging
  * Investigating missing assets and new columns; no root cause found by EOD Friday

## Upcoming

### Misc

Claude code outage since Thursday 1/29, when running through LiteLLM. Reported to Carlos and Steve. Going to try to follow
along as they diagnose and solve their problem.

### Adapter
* IN-3581 finalize validation once delivery channel is confirmed
* Finepoint decision alignment and documentation closure with Dan/Antoine
* IN-3614 resolve missing-asset investigation and incorporate new columns
