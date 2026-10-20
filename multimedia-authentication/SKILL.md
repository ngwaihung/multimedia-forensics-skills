---
name: multimedia-authentication
description: Plan and conduct question-driven forensic authentication of image, video, or audio evidence, including preservation, provenance, hypothesis testing, corroboration, and defensible reporting. Use for an end-to-end multimedia examination; use a specialist skill for a narrow task.
---

# Multimedia Authentication

Act as an examiner. Establish what the supplied material can and cannot answer before choosing tools. An anomaly is a lead, not proof of manipulation. A detector score is not an evidential conclusion.

## Examination contract

1. Record the request, the exact proposition(s) to test, the supplied items, their source and acquisition method if known, and the scope of the opinion. Ask for missing originals or comparison material when they could materially change the conclusion; continue on the available material with an explicit limitation.
2. Preserve supplied bytes. Record an identifier, size, cryptographic hash (prefer SHA-256), path or source, receipt time with timezone, handler, and every custody transfer. Perform analysis on verified working copies; record any extraction, conversion, enhancement, or export as a derivative with parent hash and exact parameters. Never overwrite the source. See [evidence integrity](references/evidence-integrity.md).
3. Form at least two plausible, testable explanations for each material anomaly, including an ordinary capture, transfer, or platform-processing explanation where applicable. Choose tests for their ability to discriminate between those explanations, not for tool availability.
4. Identify file type by bytes and parse structure and metadata before pixel, frame, or waveform interpretation. Treat metadata as user-editable claims, and account for transcoding, social-platform processing, and incomplete files. See [metadata and containers](references/metadata-and-container-analysis.md).
5. Follow only relevant modality guidance: [image](references/image-authentication.md), [video](references/video-authentication.md), [audio](references/audio-authentication.md), [synthetic media](references/deepfake-and-synthetic-media.md), or [enhancement](references/forensic-enhancement.md). Use [content provenance](../content-provenance/SKILL.md) when earlier occurrences, source history, signed claims, or producer watermarks could help test a proposition. Use the matching [image](workflows/image-manipulation-examination.md), [video](workflows/video-continuity-examination.md), or [audio](workflows/audio-splicing-examination.md) workflow when the question calls for it.
6. Corroborate material findings with a method based on a different signal or with an authentic comparison sample. Document negative and inconclusive results as well as positive ones. Separate direct observations, measurements, inferences, and assumptions.
7. Report the tested propositions, item identity, methods and versions, settings, results, alternative explanations, limitations, and a calibrated conclusion. Use [reporting guidance](references/reporting-and-limitations.md) and the [finding schema](schemas/finding-schema.json).

## Tool selection

Select the smallest set of tools that can answer the question. ExifTool parses metadata; MediaInfo summarizes streams; FFprobe/FFmpeg exposes packet and frame timing and creates documented derivatives; Python/OpenCV and signal libraries support reproducible measurements. A viewer is useful for visual inspection but its display is not a measurement. Check tool versions and preserve commands, standard output, errors, and relevant environment details. Validate tool parsing against a second parser or byte-level inspection when a contested finding depends on it. Specialist software is acceptable when its algorithm, settings, limitations, and export history can be documented.

If the submitted item is a screenshot, platform download, re-encoded clip, or otherwise remote from the acquisition original, limit source-camera and historical claims accordingly. Do not infer that an absence of detected anomalies proves authenticity. Do not identify a person, device, date, location, or generative model solely from a weak artifact or model score.

## End-to-end operating sequence

1. **Intake gate:** Inventory all submitted items, carriers, sidecars, and transfer records with [media triage](../media-triage/SKILL.md). Compute and verify hashes, preserve native bytes, and record custody gaps. A source-copy hash does not authenticate the event depicted. For imagery integrity, consult [SWGDE 17-I-001-1.1](https://www.swgde.org/documents/published-complete-listing/17-i-001-best-practices-for-maintaining-the-integrity-of-imagery/).
2. **Question gate:** Write a proposition and meaningful alternative for each requested opinion. Distinguish file provenance, capture source, content alteration, event truth, and identity. Determine whether file generation, quality, quantity, and available reference material make the question answerable. Record why any requested test is out of scope or non-diagnostic.
3. **Method gate:** Route to the matching [image](../image-authentication/SKILL.md), [video](../video-authentication/SKILL.md), [audio](../audio-authentication/SKILL.md), or [synthetic-media](../synthetic-media-analysis/SKILL.md) skill, adding [content provenance](../content-provenance/SKILL.md) where publication or processing lineage matters. For multimodal files, inspect each relevant stream; video continuity does not authenticate its audio. Select global and local tests that discriminate rival explanations. Validate tools on known samples or cross-check contested parsings.
4. **Execution gate:** Preserve exact commands, software/model versions, settings, logs, source offsets or coordinates, controls, output hashes, and errors as work occurs. Distinguish observation from measurement, and quantify uncertainty for measurements where applicable. Treat model and visualization outputs as leads until the method has case-relevant validation and independent corroboration.
5. **Challenge gate:** Test benign capture, device, export, and platform-processing explanations. Seek independent evidence or exemplars. Record material negative and contrary results. Stop or narrow the opinion when source quality, domain shift, or missing reference data defeats the method.
6. **Reporting gate:** Use [forensic reporting](../forensic-reporting/SKILL.md) and [SWGDE 18-Q-002-1.0](https://www.swgde.org/documents/published-complete-listing/18-q-002-swgde-requirements-for-report-writing-in-digital-and-multimedia-forensics/). Trace each exhibit to source and derivative history. Submit opinions for independent comparably trained review where modality guidance calls for it; an agent cannot review its own result independently. A draft remains preliminary until review and human authorization.

## Route by forensic question

| Question | Primary examination | Typical corroboration |
| --- | --- | --- |
| What is this file and how was it delivered? | [Media triage](../media-triage/SKILL.md) | Acquisition record, second parser, sidecars. |
| Where else did it appear and what lineage is supported? | [Content provenance](../content-provenance/SKILL.md) | Preserved occurrences, metadata, C2PA verification, producer watermark checks. |
| Was a still image composited or retouched? | [Image authentication](../image-authentication/SKILL.md) | Related originals, controlled exemplars, structure plus scene signals. |
| Is video continuous, original, or re-encoded? | [Video authentication](../video-authentication/SKILL.md) | Container timeline, matched device exports, independent audio examination. |
| Was audio paused, cut, or inserted? | [Audio authentication](../audio-authentication/SKILL.md) | Codec/structure plus acoustic analysis, original recording. |
| Is a component generated or face/voice swapped? | [Synthetic-media analysis](../synthetic-media-analysis/SKILL.md) | Verified provenance, modality-specific traces, locally validated detector. |
| Can an unclear feature be made more inspectable? | [Forensic enhancement](../forensic-enhancement/SKILL.md) | Source comparison and complete processing chain. |

Tool suggestions in these skills are examples, not SWGDE endorsements. Confirm exact tool behavior, version, method validity, and local laboratory procedures before using a result in a court-facing opinion.
