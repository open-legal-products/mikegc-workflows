# Contributing

Contributions to MikeGC Legal Workflows are welcome. Keep changes focused,
portable, and easy to review.

## Workflow Requirements

- Follow the repository structure documented in `README.md`.
- Keep the workflow folder, frontmatter `name`, and slug of
  `metadata.mike-display-name` aligned.
- Use only string values in `metadata`.
- Use `mike-availability: "system"` only for workflows approved to ship with
  MikeGC. New community workflows should normally use `add-on`.
- Keep instructions lightweight and harness-neutral. Do not include CLI
  commands, named harness tools, or implementation-specific object models.
- Do not invent legal conclusions that are unsupported by the source material.
- Preserve stable workflow and pack identifiers after publication.
- Store assistant workflow document templates under `assets/` and reference
  each relative path in `SKILL.md`.

## Tabular Reviews

- Define columns in `table-columns.yaml` under the root `columns` key.
- Give every column a unique name, contiguous zero-based index, supported
  format, and non-empty prompt.
- Maintain shared instructions in
  `workflow-schema/tabular-review-instructions.md`, then regenerate every
  tabular skill:

```bash
python3 workflow-schema/generate-tabular-skills.py
```

Place workflow-specific guidance in a separate heading after the generated
instruction block so regeneration preserves it.

## Validation

Run validation before opening a pull request:

```bash
python3 workflow-schema/validate-workflows.py
python3 -m unittest discover -s workflow-schema -p 'test_*.py'
```

## Licensing and Provenance

This repository is licensed under the Apache License 2.0. Unless you state
otherwise, contributions you submit are licensed under the same terms, as
described in section 5 of the license.

By contributing, you confirm that you have the right to submit the material
under its stated license. Follow `PROVENANCE.md` for adapted or third-party
workflows and `VERSIONING.md` when changing published workflows.
