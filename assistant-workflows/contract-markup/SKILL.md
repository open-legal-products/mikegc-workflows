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

Read the whole contract, including definitions, schedules, and exhibits,
before changing anything. A defined term or schedule can change how a clause
operates.

Apply the user's instructions and any playbook, standard positions, or
precedent they provide. Without a playbook, note the contract type and
governing law from the document, and ask the user once for any deal context
the materials do not show, such as what is being bought or sold, its value,
and how much risk the user will accept. Then take reasonable market-standard
positions for the user's side under that governing law. If the user gives no
context, change only provisions that create a clear legal risk for the user's
side, and list other issues under Points for Business Input instead of
changing them.

Use the markup level the user asks for, or Standard if they do not say:

- **Light** — Must-have changes only.
- **Standard** — Must-have and Important changes.
- **Full** — Must-have, Important, and Nice-to-have changes.

At every level, do not redraft for style.

If the contract cannot be edited in its uploaded format without losing
content, such as a scanned or protected PDF, stop and ask the user for an
editable version. Never return a flattened or incomplete copy.

Use an available file-copy tool call to create a copy of the uploaded
contract, then edit that copy directly. Never modify the original file. Make
every change as a tracked change so the counterparty can see it, and add a
short margin comment explaining the reason for each significant change. Write
comments for the counterparty: keep internal reasoning, fallback positions, and
negotiation strategy out of the document.

If the contract already contains tracked changes or comments, such as the
counterparty's last turn, leave them in place. Do not accept, reject, or delete
them unless the user asks. Make any counter-proposal as your own tracked change
or reply comment.

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

Use these priorities, and sort the table with Must-have changes first:

- **Must-have** — the user should not sign without this change.
- **Important** — a significant risk or cost that is worth negotiating.
- **Nice-to-have** — an improvement the user could concede.

In Location, give the clause, section, schedule, or page reference. In Fallback
Position, give the user's fallback if they supplied one. Otherwise, give a
fallback labelled "Suggested:", or write "Needs business input" where the
fallback is a commercial decision.

Include a row for each existing counterparty change, recommending whether to
accept, reject, or modify it.

After the table, list under **Points for Business Input** any issues left
unmarked because they need a commercial decision, such as pricing, service
levels, or scope.

Do not invent facts, parties, amounts, dates, or obligations. Where a change
needs information the user has not provided, insert a clearly marked
placeholder and list it in the summary.
