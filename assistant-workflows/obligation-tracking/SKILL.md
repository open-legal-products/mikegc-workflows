---
name: "obligation-tracking"
description: "Build an obligations register from executed contracts, capturing each obligation, deadline, notice window, and consequence so it can be tracked to completion."
license: "Apache-2.0"
metadata:
  version: "1.0.0"
  author: "MikeGC"
  language: "English"
  mike-display-name: "Obligation Tracking"
  mike-type: "assistant"
  mike-availability: "add-on"
  practice: "General Transactions"
  jurisdictions: "General"
---
# Obligation Tracking

## Instructions

Build an obligations register from the uploaded contracts so the in-house team
can track what must be done, by whom, and when. If no contract has been
provided, ask the user to upload the executed agreement and any amendments,
order forms, statements of work, or schedules.

If it is not clear which party the user represents, ask once. If the user does
not say, record the obligations of every party and label each one.

Read related documents together. Where an amendment or later document changes
an obligation, record the obligation as amended and cite both the original and
amending provisions.

Capture each obligation, condition, and time-limited right, including where
present:

- Payment, invoicing, and fee adjustments
- Delivery, performance, service levels, and acceptance
- Reporting, records, and audit
- Notices and consents, including change of control and assignment
- Renewal, expiry, and termination notice windows
- Compliance, including data protection, security, insurance, and regulatory
  requirements
- Confidentiality, and the return or destruction of information
- Restrictive covenants, such as exclusivity, non-solicitation, and
  non-competition
- Obligations that survive termination or expiry

Where a due date can be calculated from dates in the documents, state the
calculated date and show the calculation in Notes, for example "Expiry 31
December 2027 less 90 days' notice". Where timing depends on an event, state
it relative to that event, such as "Within 30 days of receipt of invoice". Do
not assume dates that the documents do not provide.

## Deliverable

Render the register as an exportable Excel (`.xlsx`) file. If Excel output is
not possible, render it as a Markdown table. Use exactly these columns:

- ID
- Obligation
- Obligated Party
- Category
- Trigger or Timing
- Due Date or Frequency
- Location
- Consequence of Non-Compliance
- Suggested Owner
- Notes

Group rows by contract when several contracts are provided. In Location, give
the clause, section, schedule, or page reference. In Suggested Owner, name the
function best placed to perform the obligation, such as Finance, Procurement,
Security, or Legal. In Consequence of Non-Compliance, state only the
consequence the contract provides, or "Not stated".

After the register, list **Key Dates**: the dated obligations and notice
deadlines in chronological order, highlighting any renewal or termination
notice window that could lapse without action.

Do not invent obligations, parties, dates, amounts, or consequences. Note
ambiguities, conflicts between documents, and obligations with no stated
deadline in Notes.
