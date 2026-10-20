---
name: video-authentication
description: Examine video continuity, edits, timing, and encoding history using container, packet, frame, and synchronized audio evidence. Use for a video authenticity or splice proposition.
---

# Video authentication

Clarify the requested opinion: file provenance and processing history, source device or system, or alteration of encoded content and timing. Identify any separate question about whether the depicted event actually happened; file authentication alone cannot establish that. Record the claimed recording date, device, custody, and available exemplars. Limit task-irrelevant context that could bias the examination and assess whether the requested test is suitable. Preserve and hash the submitted container, analyze a verified copy, and log extracted streams and frames as derivatives. See [evidence integrity](../multimedia-authentication/references/evidence-integrity.md).

Plan global and local tests suited to that opinion. Inspect container, binary structure, attributes, and decoded content; compare relevant device or processing-chain exemplars when possible. For a continuity claim, inspect timebases, edit lists, packet/frame timing, GOP structure, decode errors, and audio/video behavior. Distinguish observation-based findings from measurements and account for measurement uncertainty. Validate tools and cross-check material metadata interpretations with another parser. Test ordinary explanations such as variable frame rate, B-frame reordering, camera drops, in-camera pause, and platform transcode. Use [video methods](../multimedia-authentication/references/video-authentication.md) and the [continuity workflow](../multimedia-authentication/workflows/video-continuity-examination.md).

Corroborate material findings with other applicable tests or an earlier source. If the file contains audio, route the audio stream to an audio-authentication examination; visual continuity alone does not authenticate sound. Report supporting and contrary observations, technical reasoning, alternatives, and limits. State whether the result is consistent with an original, inconsistent with an original, or inconclusive under the stated proposition. Submit a final forensic opinion for independent review by a comparably trained examiner; an agent cannot independently review its own work. Until then, label it preliminary. See [reporting guidance](../multimedia-authentication/references/reporting-and-limitations.md).

## Suggested SWGDE-based examination sequence

The source is [SWGDE *Best Practices for Digital Video Authentication*, 23-V-001-1.2 (7 March 2024), §§ 4-8](https://www.swgde.org/wp-content/uploads/2026/02/23-V-001-1.2-Best-Practices-for-Digital-Video-Authentication.pdf). The URL path includes 2026, but the document's stated version date is 2024. Choose tests for contextualization, source identification, or content authentication as the request requires.

1. **Prepare the case.** Clarify the alleged camera/recording system, acquisition method, recording time, editing allegation, relevant interval, and whether the device or matching samples are available. Check custody and file originality, especially portal or third-party submissions. State competing hypotheses and whether the proposed tests can answer them.
2. **Preserve the native file.** Hash source and working copy. Inventory all tracks, sidecars, proprietary security features, timecode, and other peripheral data. Record any required vendor player and its effects. If exporting from a proprietary system, retain native bytes and document lost or changed metadata.
3. **Global examination.** Identify container and binary layout; map track/sample tables, edit lists, codec parameters, encoder markers, timestamps, color information, and duration. Distinguish embedded metadata from computed values. Cross-check contested fields with validated independent parsers or byte-level review. Compare with a device or export-chain exemplar when source is at issue.
4. **Local examination.** Build an indexed timeline of packets and presented frames (PTS, DTS, durations, keyframes, errors). Inspect visual and acoustic continuity across the disputed segment. Depending on the claim, test duplicated/missing frames, GOP or compression transitions, pixel/scene consistency, frame correlation, sensor noise, and synchronization. Separate direct observations from measured similarity or timing; document measurement error.
5. **Challenge and corroborate.** Test variable frame rate, B-frame reorder, dropped capture frames, in-camera pause, stabilization, export, and platform transcode. Compare earlier files or matched exemplars. A visible cut can be genuine editing without implying lost time or deception. Authenticate audio separately when it matters.
6. **Report and review.** Record source timebase, packet/frame indices, byte offsets, commands, versions, validation status, contrary evidence, and uncertainty. State whether results are consistent with an original, inconsistent, or inconclusive under the stated proposition. Obtain independent comparably trained review before finalizing the opinion.

## Suggested open source tools and algorithms

| Purpose | Tool or algorithm | Consideration |
| --- | --- | --- |
| Stream/packet timeline | [FFprobe](https://ffmpeg.org/ffprobe.html) `-show_streams -show_packets -show_frames` | Presentation and decoding order differ; preserve original timebases and parser errors. |
| Container metadata | [MediaInfo](https://mediaarea.net/MediaInfo), ExifTool, Bento4 or GPAC parsers | Cross-check disputed box/tag interpretations; proprietary formats may need vendor documentation. |
| Derivatives | [FFmpeg](https://ffmpeg.org/documentation.html) stream copy, lossless frame export, frame hashes | Stream copy is preferable for isolation; transcoding can erase the very trace under examination. |
| Visual measurements | [OpenCV](https://docs.opencv.org/) frame difference, optical flow, histogram/correlation | Scene changes, camera motion, auto exposure, and compression cause false discontinuities. |
| Structural/source comparison | GOP/quantization analysis, byte-layout comparison, qualified sensor-noise methods | Match device settings and export path; sensor traces may support only a class-level inference. |

For a disputed interval follow the [video continuity workflow](../multimedia-authentication/workflows/video-continuity-examination.md). Do not claim that file authentication establishes the truth of a staged or reenacted event.
