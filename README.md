# Veridence: public reference

Veridence is Agiphi's verification engine. It reads a software repository at one exact commit and reports what it finds: security problems, open-source licence obligations, risky dependencies, infrastructure misconfiguration, code that is hard to change, and how much of the code depends on one or two people. Each finding has a location, a risk rating and a cost-to-fix range.

Agiphi, Inc. builds and verifies financial infrastructure. Veridence is used for technical due diligence and for audits of trading and payments systems.

- Product: https://www.veridence.agiphi.com
- Sample report: https://www.veridence.agiphi.com/sample-report
- Methodology (every rule and every published estimate): https://www.veridence.agiphi.com/methodology
- Company: https://agiphi.com

This repository holds public documentation only. The engine's source code is not published here.

## How it works

1. **One exact commit.** An audit reads one commit of a repository, so the result can be reproduced.
2. **Code analysis.** Python, JavaScript and TypeScript are parsed into syntax trees and checked by the structure of the code: hard-coded secrets, SQL built from variables, weak hashing, `eval`/`exec`, shell commands, unsafe deserialisation, TLS checks turned off, discarded exceptions and function complexity. Infrastructure files, access policies and other languages get simpler text-pattern checks.
3. **Licences.** Licences are read from what the repository declares (licence files, manifest fields, SPDX tags) and checked against the SPDX licence list.
4. **Dependencies.** Pinned dependencies from npm, PyPI, Go, Cargo, Maven, RubyGems and Composer manifests are looked up in deps.dev for their licence and published security advisories. Only package names and versions are sent, never code.
5. **Key-person risk.** Commit history for the 12 months before the reviewed commit shows how concentrated the authorship is.
6. **Pricing.** Each finding gets a risk rating (high, medium, low) and a cost-to-fix range: published engineering hours × $175 an hour. Findings in test, example and documentation code are reported separately and are not priced.

The engine is deterministic. There is no AI model and nothing is sampled, so the same commit always gives the same report.

## What it does not claim

- Finding nothing does not prove a codebase is secure.
- A static review cannot show how a system behaves in production or under load.
- Costs to fix are engineering estimates. They are not valuations.
- Languages beyond Python, JavaScript and TypeScript get pattern checks only, with more false positives.
- The hosted service is not air-gapped. It calls the code host, Slack, deps.dev and Stripe to do its work. Code is read in memory and is not stored after the audit; only the findings are kept.
- Agiphi does not hold a SOC 2 or ISO 27001 report.

## Where it runs

- **Slack:** `/veridence audit <repository>` posts the result and a PDF report; `/veridence watch` alerts the channel only when findings change.
- **GitHub:** the [Veridence GitHub App](https://github.com/apps/veridence) adds a check to each pull request that fails only when the pull request adds findings.
- **Web account, REST API and MCP server** for teams working outside Slack.

How to connect private repositories: [docs/INGESTION-GUIDE.md](docs/INGESTION-GUIDE.md).

## Plans

A free preview shows the risk, the cost to fix and the name of every finding for one repository. Paid plans unlock locations, evidence, fixes, PDF and CSV. Current prices: https://www.veridence.agiphi.com/slack#pricing

## Research history

Veridence started as research on agentic (AI-assisted) review in April 2026 and was redesigned as a deterministic engine in August 2026. Both technical reports are preprints on ResearchGate; they are not peer-reviewed. Some terms in their titles ("air-gapped", "sovereignty") describe an earlier design and do not describe the hosted service today.

- August 2026 report: https://www.researchgate.net/publication/404363566
- April 2026 report (superseded): https://www.researchgate.net/publication/412115837

The older documents in `docs/` are kept so existing links still work; each one says what has changed.

## Contact

contact@agiphi.com · Agiphi, Inc., 30 N Gould St, Sheridan, WY 82801

### Citation

```bibtex
@techreport{agi2026deterministic,
  title={Deterministic Algorithmic Technical Due Diligence: Air-Gapped TDD, The Sovereignty Protocol, and 4-Quadrant Infrastructure Risk Quantification},
  author={Agi, Precious O.},
  institution={Agiphi, Inc.},
  year={2026},
  month={August},
  doi={10.13140/RG.2.2.17983.52648},
  url={https://www.researchgate.net/publication/404363566}
}
```

The title above is the report's published title and is kept as is for citation.
