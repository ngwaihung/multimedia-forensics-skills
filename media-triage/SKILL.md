---
name: media-triage
description: Identify and inventory submitted image, video, or audio files, preserve their bytes, and flag questions for deeper forensic examination. Use for intake and initial anomaly assessment, not a final authenticity opinion.
---

# Media Triage

Record the task question and what generation of material was supplied. Assign item IDs; preserve and SHA-256 hash each source and verified working copy. Log paths, byte counts, origin, receipt time with timezone, handler, tools/versions, commands, errors, and derivative hashes. See [evidence integrity](../multimedia-authentication/references/evidence-integrity.md).

Identify actual format from bytes, compare extension and parser results, and inventory metadata, streams, codecs, durations, timebases, dimensions, color and audio parameters. Use ExifTool, MediaInfo, FFprobe, or format-specific parsers only as relevant; consult [metadata and container analysis](../multimedia-authentication/references/metadata-and-container-analysis.md). Distinguish reported tag values from independently established facts.

Produce a short triage record: item identity and generation, observed irregularities with offsets/times, plausible benign explanations, missing originals/comparison material, and prioritized tests that could answer the user's proposition. Label leads as leads. A mismatch or absent metadata is not itself evidence of manipulation. Route substantive modality questions to the matching specialist skill or [end-to-end authentication](../multimedia-authentication/SKILL.md).

## Suggested workflow

1. **Scope.** Separate file integrity, source history, content alteration, and the truth of depicted events. Record the asserted device, capture time, delivery route, and known exports. Limit task-irrelevant case narrative that could bias later examination.
2. **Intake.** Assign case and item IDs. Record carrier or download path, submitter, handler, time with timezone, byte count, and condition. Hash at receipt and after copying. Preserve portal headers, sidecars, and acquisition details when available. Document custody gaps and errors rather than reconstructing them.
3. **Identify.** Compare extension, magic bytes, MIME inference, and independent parser results. Inventory embedded images/previews, streams, tracks, subtitles, timecodes, and peripheral data. Keep embedded tags distinct from tool-calculated values.
4. **Assess generation.** Classify as acquisition original, first removable copy, export, platform derivative, screenshot/screen recording, or unknown, stating the basis. Seek a native file or matched exemplar when it could materially alter the examination.
5. **Handoff.** For each anomaly, record the exact byte, pixel, sample, or time location; an ordinary explanation; and a test that could discriminate. Prioritize material questions for the [image](../image-authentication/SKILL.md), [video](../video-authentication/SKILL.md), [audio](../audio-authentication/SKILL.md), [synthetic-media](../synthetic-media-analysis/SKILL.md), or [content-provenance](../content-provenance/SKILL.md) skill. If no sound test is possible, state the limit.

## Suggested open source tools

| Purpose | Tool or algorithm | Consideration |
| --- | --- | --- |
| Byte identity | `sha256sum` or PowerShell `Get-FileHash -Algorithm SHA256` | A matching hash proves byte identity between observed states, not scene truth or pre-receipt history. |
| Type and metadata | `file`/libmagic; [ExifTool](https://exiftool.org/) with `-G1 -a -s -u` | Extensions and metadata are editable. Preserve raw output and parser warnings. |
| Streams and codecs | [MediaInfo](https://mediaarea.net/MediaInfo); [FFprobe](https://ffmpeg.org/ffprobe.html) `-show_format -show_streams` | Disagreeing parsers trigger format-specific review; do not choose the convenient value. |
| Byte layout | Hex viewer or Python `struct` with a format specification | Inspect a working copy and map claimed fields to offsets. |

The triage handoff includes hashes, custody status, parser versions/commands/errors, observed leads, missing material, and proposed specialist tests. For image/video preservation principles, see [SWGDE *Best Practices for Maintaining the Integrity of Imagery*, 17-I-001-1.1](https://www.swgde.org/documents/published-complete-listing/17-i-001-best-practices-for-maintaining-the-integrity-of-imagery/). Triage is not a final authenticity opinion.
