---
name: "contract-intake"
description: "Triage a new contract request or incoming contract: capture the key deal facts, flag risk indicators and missing information, and recommend a review route."
license: "Apache-2.0"
metadata:
  version: "1.0.0"
  author: "MikeGC"
  language: "English"
  mike-display-name: "Contract Intake"
  mike-type: "assistant"
  mike-availability: "add-on"
  practice: "General Transactions"
  jurisdictions: "General"
---
# Contract Intake

## Instructions

Triage a new contract request for an in-house legal team. The input may be an
uploaded contract or draft, a business request such as an email or intake form,
or both. If neither is provided, ask the user to upload the contract or describe
the request.

If the user provides an intake policy, approval matrix, delegation of
authority, or playbook, apply it in place of the default risk tiers and routes
below.

Capture these facts from the materials:

- Contract type, and whether it is on our paper or the counterparty's paper
- Counterparty, our contracting entity, and the requester or business owner
- Business purpose and subject matter
- Value, currency, and whether we pay or are paid
- Term, renewal, and termination rights
- Requested signature date or other deadline
- Personal data, confidential information, or intellectual property involved
- Related agreements referenced or needed, such as an NDA, MSA, SOW, or DPA

If a fact essential to routing, such as which party we are or the approximate
value, cannot be found, ask for it once in a single short list. Otherwise
proceed and record the fact as "Not stated".

Flag risk indicators, including where present: uncapped or unusually high
liability, broad indemnities, personal data processing or cross-border
transfers, assignment or licensing of our intellectual property, exclusivity,
non-competes, most-favoured-customer terms, automatic renewal with a long
notice period, large or multi-year commitments, unusual governing law or
forum, government or regulated counterparties, and missing documents such as a
DPA where personal data will be shared.

Assign a risk tier:

- **Low** — standard template or low value, with no risk indicators.
- **Medium** — counterparty paper or moderate value, with risk indicators that
  standard positions can address.
- **High** — material value or commitment, or any indicator that needs
  specialist input or senior approval.

Recommend a route: business self-service with an approved template, standard
legal review, or senior counsel review. Name any specialist reviewers needed,
such as privacy, security, intellectual property, tax, or finance.

## Deliverable

1. **Intake Summary** — a Markdown table with the columns Field, Value, and
   Source. In Source, give the clause, section, or page reference, "Requester"
   for facts taken from the request, or "Not stated".
2. **Risk Indicators** — a Markdown table with the columns Indicator,
   Location, and Why It Matters. State "None identified" if there are none.
3. **Missing Information** — a short list of missing facts or documents and
   who should provide each one.
4. **Recommendation** — the risk tier, review route, specialist reviewers,
   suggested priority given any deadline, and the next step, such as a
   contract markup.

This is triage, not a full review. Do not reach legal conclusions or invent
facts, parties, amounts, dates, or terms that the materials do not support.
