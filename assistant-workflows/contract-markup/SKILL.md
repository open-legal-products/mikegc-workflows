---
name: "contract-markup"
description: "Mark up a copy of an uploaded contract with tracked changes and comments reflecting the user's negotiating position, and summarise each change with its rationale and fallback."
license: "Apache-2.0"
metadata:
  version: "1.0.0"
  author: "MikeGC"
  language: "English"
  mike-display-name: "Contract Markup"
  mike-type: "assistant"
  mike-availability: "add-on"
  practice: "General Transactions"
  jurisdictions: "General"
---
# Contract Markup

## Instructions

If the user has not provided a contract, ask them to upload one. If it is not
clear which party the user represents, ask before marking up.

Apply the user's instructions and any playbook, standard positions, or
precedent they provide. Without a playbook, take reasonable market-standard
positions for the user's side. Unless the user asks for a lighter or fuller
markup, change only provisions that are material to risk, cost, or
operations; do not redraft for style.

Use an available file-copy tool call to create a copy of the uploaded
contract, then edit that copy directly. Never modify the original file. Make
every change as a tracked change so the counterparty can see it, and add a
short margin comment explaining the reason for each significant change. Write
comments for the counterparty: keep internal reasoning, fallback positions, and
negotiation strategy out of the document.

Keep edits surgical. Change the fewest words needed, and preserve the
document's format, styles, numbering, defined terms, and cross-references. When
a change adds, removes, or renumbers a definition or clause, update every
dependent reference. Keep inserted wording consistent with the contract's
existing drafting style and defined terms.

If tracked changes cannot be made in the available format, edit the copy
directly, tell the user that changes are not tracked, and rely on the change
summary below to identify every change.

## Deliverable

Return the marked-up copy in the same file format as the uploaded contract.

Then provide a Markdown table with exactly these columns:

- Priority
- Location
- Change
- Rationale
- Fallback Position

Use **Must-have**, **Important**, or **Nice-to-have** for Priority, and sort the
table with Must-have changes first. In Location, give the clause, section,
schedule, or page reference.

After the table, list under **Points for Business Input** any issues left
unmarked because they need a commercial decision, such as pricing, service
levels, or scope.

Do not invent facts, parties, amounts, dates, or obligations. Where a change
needs information the user has not provided, insert a clearly marked
placeholder and list it in the summary.
