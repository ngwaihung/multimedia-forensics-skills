---
name: synthetic-media-analysis
description: Assess whether image, video, or audio material was generated or synthetically altered, using provenance, modality analysis, and validated detectors. Use for deepfake or generative-origin questions.
---

# Synthetic Media Analysis

Define whether the proposition is full generation, a local edit, face swap, voice conversion, or reenactment. Preserve and hash source bytes and record the material's generation and custody. Seek acquisition originals, verifiable provenance, and independent versions. See [evidence integrity](../multimedia-authentication/references/evidence-integrity.md).

Inspect provenance and modality-specific signals before running a detector. Verify signed credentials and trust chains if present; absent credentials are not evidence of synthesis. Select a detector only if its version, applicable data domain, preprocessing, validation, and relevant error behavior can be documented. Log raw scores and thresholds. Test benign processing and domain shift, especially compression, low resolution, language, and capture conditions. Follow [synthetic-media methods](../multimedia-authentication/references/deepfake-and-synthetic-media.md).

Seek independent corroboration, and avoid counting related detector outputs as independent evidence. Do not infer a generator, prompt, actor, or calibrated probability from generic artifacts or an uncalibrated score. Provide an inconclusive conclusion when validation or source quality cannot support classification. Use [reporting guidance](../multimedia-authentication/references/reporting-and-limitations.md).

## Suggested examination sequence

There is no single SWGDE document here that validates a universal deepfake detector. Apply the applicable SWGDE [image](../multimedia-authentication/references/image-authentication.md), [video](../multimedia-authentication/references/video-authentication.md), or [audio](../multimedia-authentication/references/audio-authentication.md) authentication workflow. Use [NIST's synthetic-content transparency overview](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-4.pdf) and [NIST OpenMFC](https://mfc.nist.gov/) for detector evaluation concepts, not case-specific proof.

1. **Define the claim.** Distinguish wholly generated image/audio/video, face swap, lip sync, voice conversion, local generative fill, and conventional editing. Define the disputed region or time span and the likely source generation. Specify rival explanations such as transcoding, denoising, beauty filters, animation, or an in-camera artifact.
2. **Preserve and trace provenance.** Hash the supplied file and derivatives. Seek camera/recorder originals, project files, export logs, related frames, independent captures, and known publication history. Use [content provenance](../content-provenance/SKILL.md) for reverse lookup, lineage, metadata, C2PA, and producer-specific watermarks. Validate content binding, signature, certificate/trust status, and claim chain; distinguish a valid signed claim from the truth of every assertion within it. Absence of a manifest is non-diagnostic.
3. **Inspect modality signals.** For images, assess scene geometry, lighting, texture, compression, sensor traces, and local boundaries under the image workflow. For video, compare temporally sampled and candidate frames, motion, codec structure, and audio/video synchrony. For audio, assess encoding, room tone, spectral and prosodic continuity. Document controls and ordinary explanations.
4. **Use models only where validated.** Select a detector or watermark verifier specific to the proposition and media domain. Pin code commit, model checkpoint hash, preprocessing, threshold, sampling, and runtime. Evaluate it on independent authentic and synthetic examples matched for resolution, compression, language, demographic and capture conditions where relevant. Report false-positive and false-negative behavior at the selected threshold; do not import a benchmark accuracy number as the case error rate.
5. **Challenge the result.** Test sensitivity to resizing, recompression, crop, frame selection, and other ordinary transformations. Examine whether two detectors share training data or architecture and therefore correlated errors. Seek independent provenance or physical/structural corroboration. If no applicable validation or independent support exists, report features and an inconclusive classification.
6. **Report and review.** Record raw model scores, decision rule, per-frame or per-region outputs, failed inputs, and contrary results. State the narrow proposition supported. Submit a final forensic opinion for independent qualified review; mark an unreviewed result preliminary.

## Suggested open source tools and models

| Purpose | Tool or algorithm | Consideration |
| --- | --- | --- |
| Signed provenance | [c2patool](https://github.com/contentauth/c2patool) and the [C2PA specification](https://spec.c2pa.org/specifications/) | Verify signature and trust chain; a credential records claims, not an independent eyewitness account. |
| Structure and media samples | ExifTool, FFprobe/FFmpeg, OpenCV, Python signal libraries | Preserve original bytes and time/coordinate mapping; platform derivatives weaken source tests. |
| Face manipulation screening | [DeepfakeBench](https://github.com/SCLBD/DeepfakeBench) implementations such as Xception or Face X-ray | Research models are leads until locally validated for this generator, population, and processing path. |
| Dataset-level evaluation | [NIST OpenMFC](https://mfc.nist.gov/) task data and scoring concepts | Benchmark rank or AUC does not calibrate an individual case probability. |
| Generator-specific watermark | Publisher-provided verifier with documented key/version | A missing mark does not prove non-generation; crops and transcoding may destroy it. |

Do not claim a particular generator, prompt, author, or capture device from a generic visual artifact or model score. See [synthetic-media method limits](../multimedia-authentication/references/deepfake-and-synthetic-media.md).
