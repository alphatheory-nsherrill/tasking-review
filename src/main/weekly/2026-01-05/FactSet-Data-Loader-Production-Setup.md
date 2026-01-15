# FactSet Data Loader - Production Setup

**Type:** Bug | **Feature** | Exploration | Other
**Est:** [X]h | **Confidence:** [X]%

## Problem & Goal
FactSet Data Loader currently exists in staging as a set of stored procedures in the fds.fgp database. Need to explore this functionality independently, then coordinate with Mike to establish database parity in production to enable running this data loader in production environment.

New requirements: Explore integration with FactSet's cloud data formats (snowflake files, datalake files, parquet files) and investigate cloud utilization strategies. Additionally, explore how we can get one guy to manage both environments, instead of a single instance per environment.

## Deliverables
- Understanding of current FactSet Data Loader functionality and dependencies
- Cloud integration strategy for FactSet data formats (snowflake, datalake, parquet files)
- Multi-environment management approach (single person managing both environments)
- Production database setup plan with Mike
- Working FactSet Data Loader in production environment with cloud integration capabilities

## Entry Points
*Key components and resources to understand first*
- Staging environment: fds.fgp database stored procedures
- Current FactSet Data Loader stored procedure implementation
- Database schema and dependencies in staging
- FactSet's cloud data offerings: snowflake files, datalake files, parquet files
- Current cloud infrastructure and integration capabilities
- Multi-environment management patterns and tools
- Mike's knowledge of production database setup requirements
- Production environment constraints and requirements

## Plan
*High-level approach - bullet points preferred*
- Explore FactSet Data Loader stored procedures in staging (fds.fgp database)
- Document current functionality, data sources, and dependencies
- Research FactSet's cloud data formats (snowflake, datalake, parquet files) and integration options
- Investigate cloud utilization strategies for data loading process
- Design multi-environment management approach (single operator for both environments)
- Analyze staging vs production database differences
- Schedule time with Mike to review findings and plan production setup
- Work with Mike to establish database parity in production
- Implement cloud integration capabilities where applicable
- Test and validate enhanced FactSet Data Loader in production environment

---

## Execution Notes
*Fill as you work - blockers, discoveries, pivots*

Alex co-opted lead on this issue - my role in this transitioned from being a point of contact to being a source of
support for Alex in setting up queries and understanding database structure.

### Themes

## Time Spent
**Actual:** 1.5h (Research: 1.5h | Implementation: [X]h)

## Retrospective
**What went differently than planned?**

**Key learnings or gotchas:**