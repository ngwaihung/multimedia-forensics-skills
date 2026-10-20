# Contributing to Multimedia Forensics Skills

**Do not include sensitive, confidential, or classified information from your own or your organization's standard operating procedures (SOPs). Share general, professional guidance that others can use without revealing restricted procedures, case details, or internal controls.**

Digital forensics examiners, practitioners, researchers, developers, and technical writers are welcome to contribute. Useful contributions include corrections, clearer decision points, updated references, reproducible workflows, tool or schema fixes, and new skills that address a distinct examination question.

This suite provides instructions for an examiner or agent. A contribution should help a reader ask a testable question, preserve and identify the material, choose suitable methods, challenge alternative explanations, and report what the results do and do not support. It must not imply that a skill, tool, model, or schema can replace method validation, applicable laboratory procedures, qualified review, or human authorization of a forensic opinion.

## Find the right place for your contribution

Read the [README](README.md) and the relevant existing `SKILL.md` before starting. The nine skill directories cover orchestration, triage, image, video, audio, synthetic media, provenance, enhancement, and reporting. Shared methods and workflows live under [`multimedia-authentication/`](multimedia-authentication/), while the root [`skills.md`](skills.md) is a self-contained, single-file version of the suite.

- **Correction or clarification:** Open an issue or a focused pull request. Identify the affected passage and explain the practical consequence.
- **New method or reference:** Add it to the relevant existing skill, reference, or workflow when it serves the same forensic question. Explain when it is useful, its prerequisites, and its limitations.
- **New skill:** Propose a separate directory when the task has a distinct trigger, examination question, and output that the existing skills cannot describe clearly. An issue is helpful for discussing scope or overlap before writing a large contribution.
- **Tool, script, or schema change:** Describe the expected input and output, dependencies, failure behavior, and how you checked it. Keep supporting code small enough to inspect and reproduce.

## Write for defensible examinations

1. **State the question and alternatives.** Separate observations from interpretations. Include ordinary capture, transfer, editing, export, or platform-processing explanations where relevant. Do not turn an anomaly into a conclusion without testing alternatives.
2. **Protect the evidence trail.** Tell readers when to preserve source bytes, work on verified copies, record hashes and source generation, and track derivatives with settings and parent items. Examples should not suggest altering an original.
3. **Make methods reproducible.** Name the tool or method, the relevant version or version-dependent behavior, input requirements, settings, output to retain, controls or exemplars, and known failure modes. Do not invent commands, flags, tool output, citations, or test results.
4. **Bound the claim.** Distinguish what a method detects from what it proves. A metadata field, visualization, detector score, absent credential, or schema-valid record alone does not establish authenticity, synthesis, source, identity, or event truth. State uncertainty and conditions under which the method is inconclusive.
5. **Support technical guidance.** Where applicable, add references to relevant publications, peer-reviewed academic papers, SWGDE guidelines, primary standards, and official tool documentation that support the specific claim. Give the title, author or issuing body, version or date, and relevant section or page when available. Check that links and guidance remain current; do not describe a cited guideline as endorsing a tool unless it does.
6. **Write for use at the bench.** Give clear decision points and outputs rather than a long list of possible tools. Define specialized terms, keep the steps proportional to the question, and show what to record when a test cannot be run.

Respect jurisdictional authority, laboratory policy, privacy, and disclosure rules. Do not commit confidential case material, personal data, credentials, restricted media, or evidence from an active case. Use synthetic, licensed, or otherwise shareable examples, and document how an example was made and what it can demonstrate. Obtain permission before contributing material from another person or organization.

## Repository structure and new skills

Put a new skill in a lowercase, hyphenated directory with a `SKILL.md`. Follow the existing frontmatter format and make the description say what the skill does, when to use it, and which nearby skill handles an adjacent question. For example:

```markdown
---
name: example-examination
description: Examine a defined multimedia question using stated methods. Use when the question concerns this task; use an existing specialist skill for adjacent tasks.
---

# Example Examination

State the proposition, inputs, prerequisites, workflow, alternatives, outputs, and limitations.
```

Keep detailed material in appropriately named `references/`, `workflows/`, `schemas/`, or `tools/` files when it would make `SKILL.md` hard to follow. Use relative links that work from the file's location. The nine existing skill directories depend on their sibling layout, so check links after moving or adding files.

Update the README's skill list and routing guidance when a new skill changes how readers select a module. If a contribution changes core instructions that also appear in the root [`skills.md`](skills.md), update the aggregate so single-file users receive the same guidance. The aggregate must remain understandable without access to the modular files.

## Check your work before a pull request

There is no repository-wide automated validation gate documented here. Check the parts your change affects and report what you actually verified:

- Read the revised instructions end to end and follow the proposed route with a representative, shareable scenario. Confirm that the question, inputs, actions, records, alternatives, limits, and output are clear.
- Run any commands or scripts you introduce on suitable known samples. Record the tool versions and observed result. If you cannot run a method, say so in the pull request and narrow the claim.
- Check local Markdown links, frontmatter names, and references to moved files. If you change a JSON schema, parse it and validate representative valid and invalid records.
- Check that cited documents and tool options exist at the stated version, that copied text and media may be shared, and that the root aggregate and README agree with affected modules.
- Have a qualified colleague review material technical claims when possible. Describe the review performed; do not represent an agent's self-review as independent review.

## Submit a pull request

Fork the repository, create a focused branch, and open a pull request against the repository's default branch. A focused change is easier to check; include related README and aggregate updates in the same pull request. In the description, provide:

1. The forensic question or documentation problem and who the change helps.
2. What changed, where it belongs in the suite, and any overlap with existing skills.
3. The sources, tool versions, samples, checks, and observed results supporting material claims.
4. Limitations, unanswered questions, and any effect on existing workflows or schemas.
5. Attribution for adapted material and disclosure of relevant vendor, product, or project affiliations. If AI assisted with drafting or code, say how you verified its output.

Review comments may ask for a narrower claim, stronger citation, reproducible check, or clearer separation of observation and inference. Please respond with evidence or revise the guidance. Keep discussion respectful and focused on the work.

For questions, uncertain scope, or a correction that needs discussion, open an issue with the relevant file and section. Do not post sensitive case details in an issue or pull request.
