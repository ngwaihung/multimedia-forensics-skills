---
name: multimedia-forensics-skills
description: Conduct question-driven image, video, audio, synthetic-media, and content-provenance examinations with preserved evidence and defensible reporting.
---

# Multimedia Forensics Examination Suite

Use this single-file skill when a case concerns the authenticity, processing history, or provenance of digital image, video, or audio. It combines the nine modular skills in this repository for systems that import one file. Act as a forensic examiner: define a testable proposition, preserve the submitted bytes, select methods for that question, challenge apparent anomalies, and report the limits of the opinion. Apply current laboratory procedures, legal authority, and guidance for the jurisdiction. This file supplies an examination method, not a substitute for method validation, independent qualified review, or human report authorization.

## Route by question

| Question | Examination module | Add when relevant |
| --- | --- | --- |
| What was submitted, and what generation is it? | Media triage | Metadata/container analysis and custody record |
| Was a photograph altered or composited? | Image authentication | Content provenance, synthetic-media analysis |
| Is a recording continuous or from the claimed system? | Video authentication | Audio authentication for its sound track |
| Was sound inserted, removed, or rearranged? | Audio authentication | Video timeline, recorder exemplars |
| Was material generated or synthetically changed? | Synthetic-media analysis | Image/video/audio methods and content provenance |
| Where else did the content occur, and what lineage is supported? | Content provenance | Relevant authentication module |
| Can a feature be clarified for inspection? | Forensic enhancement | Relevant source examination |
| Is an opinion ready to communicate? | Forensic reporting | Independent qualified review |

For each request, separate **byte integrity**, **file/source history**, **content alteration**, **identity**, and **truth of the depicted event**. They are distinct propositions. A hash proves byte identity between observed states; a valid provenance credential supports a signed claim bound to bytes; neither proves the event happened. An anomaly is a lead, and a detector score is not an evidential conclusion.

## Examination contract: all modules

1. **Intake and scope.** Record case and item IDs, exact question, asserted source and delivery path, authority, received material, acquisition method, and whether each item is a native original, first removable copy, export, platform derivative, screenshot, or unknown. Limit irrelevant case narrative that could bias interpretation. Request an earlier generation, related image series, recorder/camera exemplar, project file, or acquisition record when it could materially change the opinion; continue with an explicit limitation if unavailable.
2. **Preserve.** Record filename, source path/URI, byte count, receipt time and timezone, submitter, handler, SHA-256, packaging/sidecars, and custody transfers. Hash at intake and verify each working copy. Keep submitted bytes unchanged and work on verified copies. If copying or hashing fails, stop processing that item and document the failure. Do not invent pre-receipt custody or silently repair a damaged file.
3. **Log contemporaneously.** Maintain an append-only record of actor, timestamp/timezone, action, input item/hash, exact tool/model and version, command/settings, output item/hash, warnings/errors, and result. Give extracted frames, demuxed streams, crops, plots, transcripts, and enhancements unique derivative IDs with parent links. Preserve original coordinates, sample indices, timebase, color properties, and transformation mappings.
4. **Write hypotheses before tests.** For each material anomaly, record the proposed alteration and at least one plausible ordinary explanation (capture behavior, in-camera processing, export, codec, platform transcode, or recording environment). Choose tests by their ability to distinguish these explanations. State in advance when source quality, file generation, or lack of validation makes a test non-diagnostic.
5. **Inspect structure and content.** Identify type from bytes; compare extension and independent parsers. Distinguish embedded metadata claims from tool-derived values. Inspect the scene or signal globally, then target disputed regions/intervals. Use controls, related files, or matched exemplars where feasible. Cross-check a contested parse with a second parser or byte-level format review.
6. **Challenge and corroborate.** Seek a method based on a different signal or independent source. Re-run ordinary processing scenarios where informative. Record negative, failed, inconclusive, and contrary results. Do not count two highly related models or two metadata tags from one exporter as independent support.
7. **Conclude and review.** Distinguish direct observation, measurement, interpretation, assumption, and conclusion. State the proposition actually tested and uncertainty. An absence of detected anomalies does not certify authenticity. Mark an agent-produced opinion **preliminary/unreviewed** until an independently qualified examiner reviews it and a responsible person authorizes the final report.

## 1. Media triage and file structure

**Workflow.** Inventory every item, carrier, sidecar, embedded preview, stream, track, subtitle, timecode, and proprietary security feature. Check magic bytes/header/footer, file completeness, parser errors, and extension agreement. Extract namespaced EXIF/XMP/IPTC/maker-note, QuickTime/ISO BMFF, ID3/BWF, filesystem, and platform fields as applicable. Inventory codec/profile, dimensions, sample/frame rate, timebase, duration, rotation, color information, audio layout, bitrate, encoder tags, and timestamps. For MP4/MOV questions, inspect relevant `moov`, `mdat`, sample tables, edit lists, and fragmented boxes; other containers need their own specification. Compare timestamps only after identifying clock, timezone, granularity, export, and download semantics. Decide which specialist tests could answer the question and where they should focus.

**Tools and limits.** SHA-256 (`sha256sum` or PowerShell `Get-FileHash`); `file`/libmagic; ExifTool `-G1 -a -s -u`; MediaInfo; FFprobe `-show_format -show_streams`; hex viewer or format-specific parser. Preserve full outputs, commands, versions, and errors. A mismatch, absent tag, encoder string, or filename is not by itself proof of editing, device identity, or actor identity. A source-camera claim needs matched device/export exemplars when available. Triage yields leads and proposed tests, not a final authentication opinion.

## 2. Image authentication

Based on [SWGDE *Best Practices for Image Authentication*, 18-I-001-2.0 (3 March 2025)](https://www.swgde.org/wp-content/uploads/2025/03/2025-03-03-Best-Practices-for-Image-Authentication-18-I-001-2.0.pdf). Consider **both image structure and scene content**; choose tests for the proposition rather than applying every filter.

1. Define whether the claim is scene alteration, specified manipulation, or capture-source consistency. Assess resolution, focus, lighting, compression, file generation, and the availability of RAW/JPEG originals or related image series. Record why an opinion must be limited if these are missing.
2. Examine format, metadata, thumbnails, color profile, orientation, compression tables, embedded objects, processing history, and available C2PA credentials. Verify a credential's binding and signature before interpreting its assertions; examine ingredients and trust status under the provenance module.
3. Inspect native image and controlled magnification for geometry, perspective, scale, lighting/shadows/reflections, depth of field, lens distortion, chromatic aberration, physical interaction, and series continuity. Record source pixel coordinates. A staged scene and a digitally altered file are different issues.
4. Where discriminating, test JPEG quantization/block changes or double compression; resampling periodicity; copy-move correspondences; CFA/demosaicing and local noise/PRNU; edges and compositing boundaries. Compare suspect regions with matched control regions and, ideally, exemplars from the claimed processing chain.
5. Test benign HDR, sharpening, denoising, local editing, saturation, lens effects, export, and platform recompression. Seek a different signal or earlier file. Report supporting and contrary results together, then obtain independent qualified review.

**Tools and limits.** ExifTool, c2patool, ImageMagick, OpenCV/scikit-image, JPEG quantization parsers, and controlled PRNU/CFA methods can assist. Preserve algorithm parameters, masks, thresholds, preprocessing, and output hashes. Error-level analysis, isolated block differences, noise patterns, and unvalidated sensor matching are screening observations, not a splice verdict. Recompressed or small images may defeat these tests. Do not assign unsupported numeric probabilities.

## 3. Video authentication

Based on [SWGDE *Best Practices for Digital Video Authentication*, 23-V-001-1.2 (document dated 7 March 2024)](https://www.swgde.org/wp-content/uploads/2026/02/23-V-001-1.2-Best-Practices-for-Digital-Video-Authentication.pdf). The URL path is dated 2026; cite the version date printed in the document. Distinguish contextualization, source identification, and content authentication.

1. Record alleged system, acquisition/export route, disputed interval, recording-time claim, available native file, device, and matched exemplars. State original/edited and ordinary alternatives before measurement.
2. Preserve the native container and all tracks, sidecars, security data, and vendor requirements. If a proprietary export is needed, retain native bytes and log what the export changes or loses.
3. Globally map container/box layout, tracks, codec parameters, encoder markers, edit lists, timebases, color information, duration, and metadata. Cross-check contested fields. Compare structural fingerprints with matched device/export samples only when acquisition conditions are comparable.
4. Build an indexed local timeline of packets and presented frames: byte offsets, PTS, DTS, duration, keyframes, frame index, decode errors, and source timebase. Examine visual continuity, repeated/missing frames, GOP/quantization transitions, scene changes, frame correlation, sensor/noise behavior, and audio/video synchronization around the interval.
5. Test variable frame rate, B-frame reordering, dropped capture frames, in-camera pause, stabilization, player display errors, export, and platform transcode. A visible cut may establish a transition while leaving whether time was removed unresolved. Examine relevant audio under the audio module.
6. Report time/index mapping, measurements and error, original/derivative relationships, contrary evidence, and whether the findings are consistent with an original, inconsistent with one, or inconclusive under the stated proposition. Obtain independent qualified review.

**Tools and limits.** FFprobe `-show_streams -show_packets -show_frames`, FFmpeg documented stream copy or lossless frame extraction, MediaInfo, ExifTool, Bento4/GPAC, and OpenCV frame difference/optical flow/correlation. Preserve parser warnings and original timebases: presentation order differs from decoding order. Motion, exposure, scene cuts, compression, and transcoding cause false discontinuities. A video file cannot establish that a depicted event was unstaged.

## 4. Audio authentication

Based on [SWGDE *Best Practices for Digital Audio Authentication*, 15-A-001-1.3](https://www.swgde.org/documents/published-complete-listing/15-a-001-swgde-best-practices-for-digital-audio-authentication/).

1. Specify whether the claim concerns recorder origin, capture time, pause/resume, deletion, insertion, rearrangement, or words heard. Record microphone, settings, environment, transfer path, and custody. Seek the first removable recording and recorder/export exemplars. A decoded WAV from a lossy file cannot answer original-container questions.
2. Inventory container, codec, encoded frames/chunks, channels, sample rate, bitrate, duration, timestamps, security features, and errors. For proprietary systems, examine player, checksums, logs, and export behavior. Obtain authority before testing a device that may be changed by the test.
3. Listen to the unprocessed recording at normal speed, each relevant channel, and annotate voices, ambience, reverberation, transmission noise, gaps, and recorder behavior. Log playback setup and source sample indices.
4. Select global tests where assumptions hold: metadata/chunk comparison, quantization and bit-depth trajectory, DC offset, spectrum, codec/MDCT characteristics, compression history, or electric-network-frequency trace. Validate on appropriate controls and state uncertainty.
5. At candidate boundaries, inspect waveform, short-time power, spectrogram, phase/channel coherence, codec frames, and ambient continuity. Change-point statistics locate leads; compare control intervals. Test gain control, voice activity detection, denoising, packet loss, clipping, microphone motion, and natural pauses.
6. Corroborate structurally and acoustically, or against earlier audio/synchronized video. Report boundary sample indices and source times with uncertainty, contrary evidence, and independent review status.

**Tools and limits.** FFprobe/MediaInfo/ExifTool for structure, FFmpeg stream copy and documented PCM derivatives, Audacity/Sonic Visualiser for inspection, NumPy/SciPy/librosa for STFT, RMS, DC offset, and channel correlation. Record window/overlap/filter/rate choices. Enhancement can create apparent features; it cannot alone establish exact words or speaker identity.

## 5. Synthetic-media analysis

Use the relevant SWGDE image, video, or audio authentication process above. [NIST synthetic-content transparency](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-4.pdf) and [NIST OpenMFC](https://mfc.nist.gov/) inform evaluation; neither validates a universal detector for a particular case.

1. Define full generation, local generative edit, face swap, lip sync, voice conversion, or reenactment, including the disputed region/time. Record non-synthetic explanations such as codec artifacts, beauty filters, denoising, and animation.
2. Preserve source bytes and seek originals, independent captures, production/project records, publication history, credentials, and supported producer watermarks. Apply the provenance module; no credential or watermark is non-diagnostic.
3. Examine modality signals: image geometry/lighting/texture/structure; video temporal behavior, codec and synchronization; audio encoding, room tone, spectral and prosodic continuity. Use matched controls.
4. Only use a classifier for an applicable domain after recording code commit, checkpoint hash, preprocessing, frame/region sampling, threshold, runtime, and validation on independent authentic and synthetic samples matched for resolution, compression, language, demographic/capture conditions where relevant. Record false-positive and false-negative behavior at the chosen threshold. Benchmark AUC is not a case probability.
5. Test sensitivity to crop, resize, recompression, and frame selection; check whether detectors have correlated training or architecture. Seek independent physical, structural, or provenance support. Without applicable validation and corroboration, report observed features and an inconclusive classification.

**Tools and limits.** c2patool; ExifTool/FFprobe/FFmpeg/OpenCV; research implementations such as DeepfakeBench/Xception or Face X-ray for screening; provider-specific watermark verifiers. A model score cannot identify a generator, prompt, person, author, or exact probability without a supported attribution method. Keep raw scores and failures.

## 6. Content provenance

This module supplements authentication. Define whether the target is earliest **known** occurrence, likely upstream file, lineage, claimed device, publisher, or AI-tool involvement. A first indexed result is not necessarily first publication or capture.

1. Preserve the supplied file and establish its exact SHA-256. Derive documented pHash/dHash or visual features for images/selected video frames, and acoustic fingerprints where suitable. These retrieve candidates; verify matches manually using distinctive content, geometric/temporal alignment, and transformations.
2. Search whole images and distinctive crops through independent indexes when justified; search OCR text, captions, filenames, and logos. For video, search selected opening, middle, closing, and disputed keyframes plus transcript/title phrases. For audio, search distinctive speech/music text or an authorized fingerprint index. Log query, crop/frame hash, service, settings, result URL, account, snippet, and query time/timezone. Search ranking and coverage are not chronology.
3. Where authorized, preserve candidate page and media bytes, URL/platform ID, account claim, asserted publication/modification times, retrieval time, headers/API response, and page capture. Prefer native media download; label platform transcodes. Do not upload nonpublic evidence to public search or watermark services without case authority and a disclosure decision.
4. Compare exact hashes, duration, dimensions, crops, overlays, unique defects, compression generations, frame order, and sound track. Build a candidate lineage: files as nodes and observed transformations as evidence-backed edges. Distinguish exact byte copy, supported derivative, and mere content match. An upscale may look higher resolution than its source.
5. Compare embedded EXIF/XMP/IPTC/QuickTime/ID3/BWF, device/software/encoder, original filename, edit history, GPS, thumbnails, timezones, filesystem/platform times, and sidecars. Treat tags as editable claims; two tags from one exporter are not independent evidence. Reconcile clock and export behavior.
6. On the preserved bytes, use a current C2PA verifier (for example c2patool) and record manifest availability, active and ingredient manifests, content binding, claim/signature result, signer identity, certificate trust-list identity, timestamp/revocation status where available, actions, `digitalSourceType`, and broken links. Distinguish embedded, sidecar, remote, absent, and verifier-error states. A valid signature binds a claim to tested bytes but does not prove every historical assertion or scene truth. An absent/stripped credential is non-diagnostic.
7. For a producer watermark such as Google SynthID, use only an official verifier covering the claimed producer and media type when accessible. Record service/version, submitted bytes or derivative, detected region/time, full response, coverage, transformations, and known error behavior. A positive supports only the verifier's narrow detection claim; a negative does not exclude synthesis. Treat unverified third-party “SynthID detector” claims as screening.
8. Deliver an evidence-backed chronology and candidate lineage, separating earliest located, earliest independently documented, and original capture. Report contrary matches and unresolved gaps; obtain independent qualified review for a court-facing opinion.

**Tools and limits.** SHA-256; ImageHash pHash/dHash and OpenCV feature matching; FFmpeg frame extraction; Chromaprint for suitable audio; Google Lens/TinEye/platform and text search where authorized; ExifTool/MediaInfo/FFprobe; c2patool and [C2PA specifications](https://spec.c2pa.org/specifications/); an official [SynthID verifier](https://deepmind.google/models/synthid/) if available. Fingerprint similarity, snippets, “first seen” dates, credential badges, and watermark scores do not by themselves establish source attribution.

## 7. Forensic enhancement

Use [SWGDE *Image Processing Guidelines*, 15-M-002-1.0](https://www.swgde.org/documents/published-complete-listing/15-m-002-swgde-image-processing-guidelines/) and [*Best Practices for Enhancement of Digital Audio*, 20-A-001-2.0](https://www.swgde.org/documents/published-complete-listing/20-a-001-2/) where relevant; check current versions for case use.

1. State the feature/measurement to clarify, source location, intended use, and likely artifacts. Inspect unprocessed source first, including exposure, blur, interlace, compression, color, channels, spectrum, and noise.
2. Choose a minimal, parameter-driven chain: e.g. orientation, levels, deinterlacing, stabilization, conservative denoise, or audio de-click/noise reduction/equalization. Test on representative intervals/regions; order is case-specific.
3. Process only verified copies. Record operation order, masks, interpolation/kernel/window, color conversion, sample rate, codec, software/version, intermediate/output hashes, and original-to-output mapping. Retain unsuccessful settings when they affect interpretation.
4. Compare source and derivative at matched coordinates/playback level. Inspect halos, ringing, false edges, clipping, altered aspect ratio, and removed audio residual. Measure on the source when a transformation changes the property measured.
5. Label every exhibit enhanced and show the source alongside it. Generative restoration, super-resolution, source separation, and interpolation may guide investigation but cannot establish a recovered face, word, or detail absent independent source support.

**Tools and limits.** FFmpeg filter graphs, OpenCV/scikit-image, Audacity, and SciPy. Preserve exact parameters and outputs. Visual improvement is not proof that newly visible detail existed in the source.

## 8. Findings and reporting

Apply [SWGDE *Requirements for Report Writing in Digital and Multimedia Forensics*, 18-Q-002-1.0](https://www.swgde.org/documents/published-complete-listing/18-q-002-swgde-requirements-for-report-writing-in-digital-and-multimedia-forensics/) and local report rules.

1. Reconcile the request, authority, custody, source hashes, working-copy verification, notes, tool logs, validation record, raw data, derivatives, and exhibit hashes. Do not reconstruct a missing step as fact.
2. For **each material finding**, record: finding ID; proposition; item ID/hash/generation; source pixel/sample/frame/time location and timebase; observations; measurements and uncertainty; methods/tools/versions/settings/results; interpretation; at least one alternative and its test/result; corroborating and contrary evidence; limitations; conclusion category; and review status. A JSON schema validator can check field completeness, not scientific validity.
3. Draft a report with title, laboratory/address, case ID, page accountability, final date, requester/authority, purpose and scope, unique item identification, collection/submission dates and methods, processes/results/supporting data, opinion bases, evidence/derivative disposition, authorizer/signature, subcontracted work, and SOP deviations as required. Explain technical terms for a lay reader.
4. Trace every figure, crop, clip, transcript excerpt, and number to source hash, original coordinates/timebase, exact processing step, and output hash. Include material negative, failed, inconclusive, and contrary tests. Tool-generated reports remain supporting data.
5. Use bounded language such as “supported by the specified tests,” “inconsistent with the stated source claim,” “no indication detected under these tests,” or “cannot determine.” Do not supply percentages without a validated statistical model, or infer motive, legal admissibility, author, device, identity, or event truth beyond the examination.
6. Record independent reviewer qualification, date, scope, and disagreement resolution. An agent cannot review its own work independently. Leave a report preliminary until qualified review and human authorization. An amendment identifies changes and references the prior final report.

## Tool-selection rule

Use the smallest validated set that can discriminate the live hypotheses. Record version, exact invocation, settings, environment, output, errors, and material limitations. ExifTool reads metadata; MediaInfo summarizes streams; FFprobe/FFmpeg exposes packet/frame timing and creates documented derivatives; OpenCV/scikit-image and NumPy/SciPy support reproducible measurements; c2patool checks signed content provenance. Specialist software is acceptable when its method, settings, validation, and export trail can be documented. These are candidate tools, **not SWGDE endorsements** or instructions to run all tools on every item. If a required tool or reference is unavailable, state which question remains unanswered and narrow the opinion.

## Modular sources in this repository

The maintained detailed modules are [multimedia-authentication](multimedia-authentication/SKILL.md), [media-triage](media-triage/SKILL.md), [image-authentication](image-authentication/SKILL.md), [video-authentication](video-authentication/SKILL.md), [audio-authentication](audio-authentication/SKILL.md), [synthetic-media-analysis](synthetic-media-analysis/SKILL.md), [content-provenance](content-provenance/SKILL.md), [forensic-enhancement](forensic-enhancement/SKILL.md), and [forensic-reporting](forensic-reporting/SKILL.md). If this repository is mounted, consult the matching [references](multimedia-authentication/references/), [workflows](multimedia-authentication/workflows/), and [finding schema](multimedia-authentication/schemas/finding-schema.json) for more detail. The protocol above remains operative when only this one file is available. Verify current SWGDE document versions and local method validation before case use.
