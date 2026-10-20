---
name: audio-authentication
description: Examine recorded audio for splicing, inserted or removed intervals, and acoustic or encoded-stream discontinuities. Use for an audio edit proposition or audio component of a video case.
---

# Audio Authentication

Define the alleged interval and alteration. Preserve encoded source bytes, hash a working copy, identify file generation, and document any demuxing, decoding, or enhancement as a derivative. See [evidence integrity](../multimedia-authentication/references/evidence-integrity.md).

Listen at original speed, then inspect the relevant channels, encoded frames, waveform, spectrogram, phase, noise floor, reverberation, and ambient sound. Form splice and benign hypotheses; test automatic gain, noise suppression, voice activity detection, packet loss, microphone movement, and natural acoustic changes. Use control intervals and independently sourced audio or video when available. Follow [audio methods](../multimedia-authentication/references/audio-authentication.md) and the [splicing workflow](../multimedia-authentication/workflows/audio-splicing-examination.md).

Mark boundaries in source time with uncertainty. Treat filtered, slowed, separated, or generated audio as derivatives. Report observations, alternatives, contrary evidence, method settings, and limits; do not claim speaker identity or exact words from enhancement alone. See [reporting guidance](../multimedia-authentication/references/reporting-and-limitations.md).

## Suggested workflow

Based on [SWGDE *Best Practices for Digital Audio Authentication*, 15-A-001-1.3](https://www.swgde.org/documents/published-complete-listing/15-a-001-swgde-best-practices-for-digital-audio-authentication/). This guidance concerns digital audio files, not analog or live-stream authentication.

1. **Clarify the assertion.** Is the issue recorder origin, capture time, pause/resume, deletion, insertion, rearrangement, or the words heard? Record the alleged recorder, microphone, settings, environment, storage, transfer route, and custody. Seek the first removable recording or verified duplicate; a decoded WAV from a lossy original cannot answer original-container questions. Limit task-irrelevant context.
2. **Assess and plan.** Inventory codec, channels, sample rate, bit rate, duration, timestamps, security features, and parser errors. For a proprietary system, investigate its player, checksums, block structure, logs, and export behavior. Obtain authority before testing an evidence device because testing can alter its state. Write competing hypotheses and decision criteria before running signal tests.
3. **Listen before processing.** Review the unprocessed source at normal speed, annotating changes in voices, ambience, reverberation, transmission noise, recorder behavior, or gaps. Record playback equipment and channel selection. Repeat with attention to each feature.
4. **Run relevant global analyses.** Compare metadata and byte/chunk structure with recorder and export exemplars. Depending on method validation and source quality, examine quantization/bit-depth trajectory, DC offset, long-term spectrum, codec frame or MDCT behavior, compression history, and electric-network-frequency trace. Document measurement error; do not run a method whose assumptions fail.
5. **Run relevant local analyses.** Around candidate boundaries, inspect waveform, short-time power, spectrogram, channel phase/coherence, codec frames, and ambient continuity. First-difference or change-point measures can locate abrupt joins but are not splice verdicts. Compare control intervals and test gain control, voice activity detection, denoising, packet loss, clipping, microphone motion, and natural scene changes.
6. **Corroborate and conclude.** Seek an independent structural/acoustic signal, earlier recording, synchronized video, or matched exemplar. Record source sample indices and times with uncertainty. Report both supporting and contrary findings. Submit final opinions for independent qualified review; label an unreviewed opinion preliminary. Use the [splicing workflow](../multimedia-authentication/workflows/audio-splicing-examination.md).

## Suggested open source tools

| Purpose | Tool or algorithm | Consideration |
| --- | --- | --- |
| Container inventory | [FFprobe](https://ffmpeg.org/ffprobe.html), [MediaInfo](https://mediaarea.net/MediaInfo), ExifTool | Cross-check contested fields; metadata can be rewritten. |
| Demux and decoding | [FFmpeg](https://ffmpeg.org/documentation.html) stream copy; PCM derivative if necessary | Preserve encoded source, sample format, and any resampling settings. |
| Listening and plots | [Audacity](https://www.audacityteam.org/), [Sonic Visualiser](https://www.sonicvisualiser.org/) | Display and playback changes are investigative; document selection and settings. |
| Measurements | Python NumPy/SciPy or librosa: STFT, DC offset, RMS, interchannel correlation | Window, overlap, filter, and rate choices change results; validate with controls. |
