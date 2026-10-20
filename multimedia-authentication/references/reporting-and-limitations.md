# Findings and reporting

## Report structure

State instructions and propositions, evidence inventory and custody gaps, tools/versions/settings, examination steps, results, alternatives tested, limitations, and conclusions. Attach or reference hashes, logs, machine-readable outputs, and representative exhibits with original coordinates or timestamps. An independent examiner should be able to reproduce each material finding without relying on an undocumented interactive action.

Each finding should distinguish: **observation** (what the file or measurement shows), **interpretation** (what it may mean), **alternative explanations**, **supporting and contrary evidence**, **limitations**, and **conclusion**. Use [finding-schema.json](../schemas/finding-schema.json) as a record shape. Do not silently turn a preliminary lead into a final finding.

Use calibrated language tied to the evidence: supported, inconsistent with, cannot determine, or no indication detected under the stated tests. Explain exactly which proposition each conclusion addresses. If a likelihood ratio or statistical error rate is used, identify its population, assumptions, validation data, and uncertainty. Do not substitute numeric percentages or legal conclusions for unsupported certainty.

## Limits to state when relevant

Derivative-only submissions, unknown acquisition chain, incomplete or damaged files, platform recompression, absent comparison exemplars, short or low-quality clips, clock uncertainty, model domain shift, proprietary tool opacity, and non-independent corroboration. A negative result only means the specified method found no relevant indication within its sensitivity; it does not certify authenticity.

Keep the language neutral. Distinguish evidence of editing from whether editing was deceptive or material to the disputed event. Do not infer motive, authorship, identity, legal admissibility, or ultimate fact-finder conclusions from technical examination alone.

## Court-facing completeness check

[SWGDE *Requirements for Report Writing in Digital and Multimedia Forensics*, 18-Q-002-1.0](https://www.swgde.org/documents/published-complete-listing/18-q-002-swgde-requirements-for-report-writing-in-digital-and-multimedia-forensics/) lists minimum report elements. Before authorizing a final version, verify the title, laboratory name/address, case ID, page numbers and total, final date, requester and authority, purpose and scope, submission/collection dates and method, unique identity of every submitted item, process/results/supporting data, basis of opinions, disposition of originals and derivatives, and report authorizer/signature. Identify subcontracted work and deviations from SOP. Define abbreviations at first use and explain results so a lay reader can understand them without losing technical precision.

An automated tool report belongs in the case record as supporting data; it does not describe the full examination. Preserve raw output, parser errors, model checkpoints, scripts, parameter files, and intermediate derivatives needed to reproduce a material result. Audit every displayed crop, frame, waveform, or chart against original source coordinates and hashes. Reviewers must be able to trace observations through methods to conclusions, including contrary evidence.

Record whether independent review required by image, video, or audio examination guidance occurred, the reviewer's qualifications, date, scope, and disagreement resolution. An analyzing agent is not its own independent reviewer. If review has not occurred, mark opinions preliminary and leave report authorization to the responsible person or laboratory. A later amendment should identify and explain changes and reference the original final report.
