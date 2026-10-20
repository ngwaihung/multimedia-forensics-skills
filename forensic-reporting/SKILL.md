---
name: forensic-reporting
description: Turn multimedia examination records into a reproducible, technically bounded forensic report with observations, alternatives, limitations, and calibrated conclusions. Use when drafting or reviewing findings.
---

# Forensic Reporting

Identify the proposition, item IDs and hashes, file generation, custody gaps, scope, methods/versions/settings, and exhibits. For each material finding, keep observations and measurements separate from interpretation. Record the location in source coordinates or timebase, tested alternatives, corroborating and contrary evidence, limitations, and a conclusion no stronger than the tests permit. Use [reporting guidance](../multimedia-authentication/references/reporting-and-limitations.md) and the [finding schema](../multimedia-authentication/schemas/finding-schema.json).

Verify that every reported exhibit maps to a preserved source or documented derivative and that an independent examiner can repeat material steps. Explain relevant negative and inconclusive results. A negative detector result does not certify authenticity; a positive anomaly does not establish deceptive editing. Avoid unsupported percentages, author/device attribution, motive, and legal conclusions. If evidence or logs are missing, disclose that gap rather than reconstructing it as fact.

## Suggested workflow

Apply [SWGDE *Requirements for Report Writing in Digital and Multimedia Forensics*, 18-Q-002-1.0](https://www.swgde.org/documents/published-complete-listing/18-q-002-swgde-requirements-for-report-writing-in-digital-and-multimedia-forensics/). Organizational and court rules may add requirements. A tool's auto-generated report is supporting data, not a substitute for the examiner's account of the whole examination.

1. **Assemble the case record.** Collect the request and authority, chain of custody, intake hashes, working-copy verification, contemporaneous notes, tool logs, method validation, raw measurements, derivatives, exhibits, and reviewer record. Reconcile item IDs and hashes before drafting.
2. **State scope and propositions.** Give the requester, dates, exact questions, criteria for authenticity, and file generation. Identify questions outside the examination, such as the truth of a depicted event, speaker identity, or legal admissibility. Define any deviation from the agreed scope or laboratory procedure.
3. **Build a finding ledger.** For each material issue, record source location, direct observation, measurement and uncertainty, method/settings/version, interpretation, alternatives tested, supporting and contrary evidence, and limits. Use the [finding schema](../multimedia-authentication/schemas/finding-schema.json). Do not merge observations and inferences into a single assertion.
4. **Draft the report.** Include title; lab name/address; case ID; page accountability; final report date; requester and authority; unique identification of all submitted/collected items; collection or delivery dates/methods; processes, results and supporting data; basis of each opinion; evidence and derivative disposition; and authorizer/signature. Explain technical terms for a lay reader and identify subcontracted work.
5. **Audit reproducibility.** Trace every reported figure, clip, transcript excerpt, and numeric result to a source hash, command/project file, settings, output hash, and original coordinates/timebase. Check that all material failed, negative, and inconclusive tests are represented. Verify citations and table values against raw outputs.
6. **Review and authorize.** Obtain independent modality-qualified review required by the applicable examination guidance; the same agent cannot act as its own independent reviewer. Resolve disagreements in the case record. Until review and human authorization occur, mark the report a draft or preliminary opinion. Preserve a final signed version; amendments should identify and explain changes and reference the prior report.

## Suggested open source tools

| Purpose | Tool or algorithm | Consideration |
| --- | --- | --- |
| Structured findings | JSON Schema validator against the [finding schema](../multimedia-authentication/schemas/finding-schema.json) | Schema validity checks completeness of fields, not scientific validity of an inference. |
| Reproducible tables | Python/Jupyter or R with pinned packages and saved scripts | Save inputs, code, output, and environment; notebooks can hide out-of-order execution. |
| Evidence and exhibit hashes | `sha256sum` or PowerShell `Get-FileHash` | Verify actual files at report finalization, including derivatives. |
| Document generation | Markdown/Pandoc or LaTeX with versioned source | Inspect final pagination, figure labels, media references, redactions, and attachment manifest. |

Use [reporting and limitations guidance](../multimedia-authentication/references/reporting-and-limitations.md) for conclusion language. Do not express a numerical probability without an appropriate validated statistical model or substitute a technical conclusion for the court's decision.
