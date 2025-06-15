---
name: Query issue report
about: Report a query issue to help improve the project
title: 'Query issue: INSERT_QUERY_NAME'
labels: ''
assignees: ''

---

**Query reference**
 - Query name
 - Query URL or GUID

Query:
```
MATCH p=(b:You) - [h:CanReport] -> (e:Issues)
WHERE e.WellDescribed = true
RETURN p
```

**Describe the issue**
A clear and concise description of what the issue is.

**BloodHound context:**
 - Version [e.g. "BloodHound CE 7.0"]
 - Database [e.g. Neo4j or Postgres]
