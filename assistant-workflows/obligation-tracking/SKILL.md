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

Check whether each document is executed. If a document appears to be a draft
or unsigned, or its execution cannot be confirmed, say so at the top of the
deliverable and label the register "Draft — not confirmed as executed" until
the user confirms execution.

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

Where a due date can be calculated from dates in the documents, put the date
in Due Date or Frequency and the calculation in Notes. For example, enter
"2 October 2027" with the note "Expiry 31 December 2027 less 90 days'
notice". Where timing depends on an event, state it relative to that event,
such as "Within 30 days of receipt of invoice". Do not assume dates that the
documents do not provide.

For a contract that renews automatically, work forward from the original term
through each renewal to the term current at today's date. Calculate the next
expiry and notice deadline from that current term, not the original expiry,
and state the term used in Notes.

Note whether each period runs in business or calendar days, and whether notice
counts from sending or receipt. Where the contract is unclear, use the earlier
resulting date and say so in Notes.

## Deliverable

Render the register as an exportable Excel (`.xlsx`) file. If Excel output is
not possible, render it as a Markdown table. Use exactly these columns:

- ID
- Contract
- Obligation
- Obligated Party
- Category
- Trigger or Timing
- Due Date or Frequency
- Location
- Consequence of Non-Compliance
- Suggested Owner
- Status
- Notes

In Contract, name the source contract, and the amendment where one applies,
on every row. Group rows by contract. In Location, give the clause, section,
schedule, or page reference. In Suggested Owner, name the function best placed
to perform the obligation, such as Finance, Procurement, Security, or Legal.
In Consequence of Non-Compliance, state only the consequence the contract
provides, or "Not stated". Set Status to "Open" on every row for the team to
update.

After the register, list **Key Dates**: the dated obligations and notice
deadlines in chronological order. Mark any date that has already passed, and
highlight any date within the next 90 days and any renewal or termination
notice window that could lapse without action.

Do not invent obligations, parties, dates, amounts, or consequences. Note
ambiguities, conflicts between documents, and obligations with no stated
deadline in Notes.
