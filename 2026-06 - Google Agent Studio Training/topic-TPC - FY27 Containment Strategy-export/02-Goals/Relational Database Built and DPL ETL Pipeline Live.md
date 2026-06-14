---
type: goal
target_date: '2027-03-31'
topics:
  - '[[00-Topics/TPC - FY27 Containment Strategy]]'
---

## Success Criteria

- The relational database is designed, built, and accepting structured content from the Markdown editor via the DPL/ETL process
- Database type has been formally decided (Gate 0 / Decision 1 — this is the master pipeline blocker)
- Pipeline is running end-to-end: Markdown Editor → ETL/DPL → Relational DB with no manual intervention
- Downstream consumers (CRC HTML build, PDF build, Knowledge Catalog) are reading from the relational DB as their authoritative source
- Pipeline owner is named and accountable for uptime and content fidelity
