# FIGI Retrieval and Usage Research

**Type:** Bug | Feature | **Exploration** | Other
**Est:** [3]h | **Confidence:** [70]%

## Problem & Goal
Understand how a FIGI is retrieved FROM factset to request against OpenFIGI
Understand if the FIGI is requested against OpenFIGI ... ?
If not, what's the rationale?
How are we using the composite figi in TickerResolverServices?

Note: Composite FIGI only exists for Equities and potential other asset class types.

## Deliverables
Questions regarding the FIGI workflow, especially how FIGI is retrieved from factset

## Entry Points
*Key services and code to understand first*
- `OpenFigiFactSetSymbologyExtractionServices` - how it requests FactSet
- `FactSetTickerFdsWithHistoryInterpretationServices` - the target service
- `TickerResolverServices` - where FIGIs are used (focus on `figiAndTickerKey()` and `compositeOrFigi()` methods)
- Database: `select * from vendors.figi.FigiResponseInterpretationEntry`

## Plan
*High-level approach - bullet points preferred*
- Trace FIGI retrieval flow from OpenFigi → FactSet services
- Analyze the `figiAndTickerKey()` and `compositeOrFigi()` logic in TickerResolverServices
- Determine if/how FIGIs are requested against OpenFIGI API
- Document rationale for composite vs standard FIGI usage
- Query database to understand current FIGI storage/interpretation

---

## Execution Notes
*Fill as you work - blockers, discoveries, pivots*

### Themes

## Time Spent
**Actual:** [X]h (Research: [X]h | Implementation: [X]h)

## Retrospective
**What went differently than planned?**

**Key learnings or gotchas:**