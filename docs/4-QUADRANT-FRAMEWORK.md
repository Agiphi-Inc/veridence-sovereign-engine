# What Veridence checks, and how it prices findings

This page replaces an earlier "4-Quadrant" document that summed findings into an "EBITDA liability adjustment". Veridence no longer does that: single dollar totals double-counted and were not defensible.

Today every finding has:

- a **location** (file and line, where the check allows),
- a **risk rating** (high, medium, low), and
- a **cost-to-fix range**: published engineering hours × $175 an hour. A second place in the same file adds less than the first.

The checks still cover four areas:

| Area | Examples |
| --- | --- |
| Code | Function complexity, swallowed errors, hard-coded secrets, unsafe patterns (syntax-tree checks for Python, JavaScript and TypeScript) |
| Licences and dependencies | Declared licences against the SPDX list; GPL, AGPL and SSPL in production dependencies; dependency advisories rated 7.0 or higher |
| Infrastructure | Infrastructure-as-code and access-policy patterns |
| Team | Concentration of commits in one or two people over the last 12 months |

Findings in test, example and documentation code are listed separately and are not priced.

Every rule and estimate: https://www.veridence.agiphi.com/methodology
