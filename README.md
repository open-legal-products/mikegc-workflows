# MikeGC Legal Workflows

Public workflow definitions for [MikeGC](https://github.com/open-legal-products/mikegc),
the in-house legal fork of Mike. The workflows follow the
[`SKILL.md` Agent Skills specification](https://agentskills.io/specification)
used by popular agent harnesses, so they can be adapted and reused with the
agent harness of your choice.

This repository follows the structure and conventions of
[`Open-Legal-Products/mike-workflows`](https://github.com/Open-Legal-Products/mike-workflows),
so MikeGC can read workflows from either repository. It focuses on workflows
for in-house legal teams.

MikeGC imports its workflow catalog from this repository by default.

The repository has two top-level workflow collections:

- `assistant-workflows/` contains assistant workflows.
- `tabular-review-workflows/` contains tabular review workflows.

System and add-on workflows use the same simple folder structure. Their
availability is declared in `SKILL.md` rather than encoded through
additional directory nesting.

## Structure

```text
mikegc-workflows/
  assistant-workflows/
    <workflow-id>/
      SKILL.md
    <pack-id>-pack/
      pack.yaml
      <workflow-id>/
        SKILL.md

  tabular-review-workflows/
    <workflow-id>/
      SKILL.md
      table-columns.yaml
    <pack-id>-pack/
      pack.yaml
      <workflow-id>/
        SKILL.md
        table-columns.yaml

  workflow-schema/
    workflow-metadata.schema.yaml
    table-columns.schema.yaml
    pack.schema.yaml
    tabular-review-instructions.md
    generate-tabular-skills.py
    validate-workflows.py
```

Ordinary workflow folders are kept flat directly under the appropriate
top-level collection. Only workflows that belong to a pack are nested inside
their pack folder.

## Authoring Principles

Keep skills lightweight and focused instead of making them overly complicated.
Models are increasingly capable of handling general reasoning on their own, so
skill instructions should provide only the workflow-specific context,
constraints, and steps needed to produce a reliable result. Avoid unnecessary
explanation, repetition, and prescriptive detail to keep workflows
token-efficient.

Skills should not include CLI commands or commands specific to any particular
agent harness. Describe the intended action in harness-neutral language so the
workflow remains portable across compatible environments.

## System and Add-on Workflows

Every `SKILL.md` declares a `mike-availability` value inside its YAML
frontmatter metadata:

```yaml
metadata:
  mike-availability: "system"
```

Use `system` for trusted workflows that ship with MikeGC and appear as
non-editable system workflows. Use `add-on` for workflows that users can
optionally install or copy into their own workspace:

```yaml
metadata:
  mike-availability: "add-on"
```

This explicit metadata is the source of truth. Folder names should describe
what a workflow does, not how it is distributed.

MikeGC inherits Mike's workflow importer, so metadata fields keep the `mike-`
prefix used by `mike-workflows`.

## Required System Workflows

MikeGC refuses to import a catalog that is missing any of these system
workflows, which back its built-in quick actions:

- `assistant-workflows/proofread/`
- `assistant-workflows/compare-documents/`
- `assistant-workflows/extract-key-terms/`
- `assistant-workflows/draft-from-template/`
- `tabular-review-workflows/commercial-agreement-tabular-review/`

They are copied from `mike-workflows` under the MIT License, and each records
its source in `metadata` (see [PROVENANCE.md](PROVENANCE.md)). Validation fails
if one is removed or is no longer a system workflow.

## Workflow Types

### Assistant Workflows

Assistant workflows contain metadata in `SKILL.md` YAML frontmatter and
instructions in the Markdown body.

Assistant workflows can prompt users for additional information or document
uploads when needed. For example, a drafting workflow can ask the user to
provide a template or precedent before continuing. MikeGC supports these
interactive requests as part of the workflow.

### Tabular Review Workflows

Tabular review workflows contain metadata in `SKILL.md` YAML frontmatter,
workflow-level instructions in the Markdown body, and column definitions in
`table-columns.yaml`.

MikeGC does not currently use the instructions in a tabular review workflow's
`SKILL.md` when running the workflow. Users trigger tabular review runs
directly, and MikeGC applies fixed system prompts together with the workflow's
`table-columns.yaml`. The results are rendered as an interactive table in the
application UI rather than having an agent generate the presentation on the
fly.

The `SKILL.md` is included to describe the workflow and ensure that it remains
portable to other agent harnesses that use skill-based instructions. Outside
MikeGC, the skill instructs the agent to produce an exportable Excel file and
to fall back to a Markdown table when Excel output is unavailable.

The canonical baseline is maintained in
[`workflow-schema/tabular-review-instructions.md`](workflow-schema/tabular-review-instructions.md).
Every tabular review `SKILL.md` should include these instructions and may add
subject-specific guidance in a separate section where needed. After changing
the canonical baseline, regenerate the tabular skill instructions with:

```bash
python3 workflow-schema/generate-tabular-skills.py
```

The `mike-type` metadata field must agree with the top-level collection:

```yaml
metadata:
  mike-type: "assistant"
```

or:

```yaml
metadata:
  mike-type: "tabular"
```

## Packs

A pack is a named bundle of add-on workflows of the same type. Pack folders
live in the relevant workflow collection and must end in `-pack` so they are
easy for both people and MikeGC to identify.

```text
assistant-workflows/
  commercial-drafting-pack/
    pack.yaml
    draft-service-agreement/
      SKILL.md
    draft-nda/
      SKILL.md
```

The pack's `pack.yaml` lists its direct child workflow folders:

```yaml
$schema: "../../workflow-schema/pack.schema.yaml"
id: "commercial-drafting"
title: "Commercial Drafting"
description: "Add-on workflows for drafting commercial agreements."
publisher:
  name: "MikeGC"
license: "Apache-2.0"
version: "1.0.0"
practice: "General Transactions"
workflows:
  - "draft-service-agreement"
  - "draft-nda"
required_connectors: []
```

Packs may optionally declare a `practice`, a `jurisdiction`, or both to
describe the bundle. These values are non-empty strings when present.

Each listed directory must exist directly inside the pack folder, and each
workflow in a pack must declare `mike-availability: "add-on"` inside its
`metadata`. Packs should not contain system workflows. Installing a pack
installs all workflows listed in its manifest.

The pack `id` is immutable after publication and must match the pack folder
name without its `-pack` suffix. For example, `commercial-drafting-pack/` uses
`"id": "commercial-drafting"`.

Packs are type-specific: an assistant pack belongs in `assistant-workflows/`,
while a tabular review pack belongs in `tabular-review-workflows/`. This keeps
the repository flat and avoids another cross-cutting directory hierarchy.

## Skill Frontmatter

Each workflow has a `SKILL.md` file with YAML frontmatter followed by Markdown
instructions. To remain portable across compatible agent harnesses, the
frontmatter uses the standard Agent Skills fields. `name` and `description`
are required by the open specification; `license` and `metadata` are also
required for workflows in this repository.

Only fields whose meaning is specific to MikeGC use the `mike-` prefix.
General fields such as `version`, `author`, `language`, `practice`, and
`jurisdictions` remain unprefixed. Metadata values are strings for
compatibility with the Agent Skills specification. Use the author or
publishing organisation's name for `author`.

```yaml
---
name: "nda-review"
description: "Review an NDA and identify material legal and commercial issues."
license: "Apache-2.0"
metadata:
  version: "1.0.0"
  author: "Open Legal Products"
  language: "English"
  mike-display-name: "NDA Review"
  mike-type: "assistant"
  mike-availability: "system"
  practice: "General Transactions"
  jurisdictions: "General"
---
```

The workflow folder and the `name` field must both match the lowercase,
hyphenated form of `metadata.mike-display-name`. For example, a display name
of `Credit Agreement Review` uses the folder `credit-agreement-review/` and
`name: "credit-agreement-review"`. Keep these identifiers stable once
published. Because the identifier is derived from the display name, treat
`mike-display-name` as immutable after publication. A breaking rename requires
an explicit migration or alias in the consuming application.

## Reference Documents

Assistant workflows may bundle document templates and other reference
documents in the standard Agent Skills `assets/` directory:

```text
assistant-workflows/
  draft-service-agreement/
    SKILL.md
    assets/
      service-agreement-template.docx
```

Reference each document directly from the `SKILL.md` body using its relative
path:

```markdown
Use the bundled template at `assets/service-agreement-template.docx` as the
starting document.
```

Reference documents are currently supported only for assistant workflows.
Every bundled `.docx` file must be located under `assets/` and referenced by
`SKILL.md`; no additional metadata declaration is required.

Tabular review `table-columns.yaml` files use:

```yaml
$schema: "../../workflow-schema/table-columns.schema.yaml"
```

For a tabular workflow inside a pack, use:

```yaml
$schema: "../../../workflow-schema/table-columns.schema.yaml"
```

## Validation

Validate workflow metadata, canonical tabular instructions, column formats,
indexes, names, and tags with:

```bash
python3 -m pip install PyYAML
python3 workflow-schema/validate-workflows.py
```

The `Validate workflows` GitHub Actions check runs the same validation, the
validator's unit tests, and JSON Schema checks on every pull request and on
pushes to `main`.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for authoring and validation rules,
[PROVENANCE.md](PROVENANCE.md) for third-party licensing requirements, and
[VERSIONING.md](VERSIONING.md) for workflow and pack versioning.

## License

Apache License 2.0. See [LICENSE](LICENSE) and [NOTICE](NOTICE).

The schemas and validation tooling in `workflow-schema/`, and workflows whose
`license` is `MIT`, come from `mike-workflows` under the MIT License; see
[`third-party-licenses/mike-workflows-MIT.txt`](third-party-licenses/mike-workflows-MIT.txt).
