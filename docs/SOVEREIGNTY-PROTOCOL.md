# How Veridence handles code

This page replaces an earlier document called "The Sovereignty Protocol". That document described an air-gapped, RAM-only design with a "cryptographic purge". The hosted service does not work that way, so the description was withdrawn in November 2026.

What is true today:

- An audit reads one commit of a repository. The code is read in memory and is not stored after the audit; only the findings (the report) are kept.
- The service is not air-gapped. It calls the code host (for example GitHub), Slack, deps.dev (package names and versions only, never code) and Stripe.
- No AI model reads the code. The analysis is deterministic.
- Access to private repositories uses a read-only GitHub App installation or a token the customer provides.
- Reports belong to the customer's workspace. Deletion requests are acknowledged within 24 hours and completed within 48 hours.
- Agiphi does not hold a SOC 2 or ISO 27001 report.

Full details: https://www.veridence.agiphi.com/sub-processors and the privacy policy on the same site. Questions: contact@agiphi.com.
