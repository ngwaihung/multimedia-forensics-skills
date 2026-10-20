---
name: forensic-enhancement
description: Create documented image, video, or audio enhancements for forensic inspection or measurement while preserving originals and preventing invented detail from becoming evidence.
---

# Forensic Enhancement

State the perceptual or measurement question before processing. Preserve and hash the source, create verified working copies, and link every output to its parent hash. Record operation order, exact parameters, software/version, source coordinates or times, color and sampling changes, and output hashes. See [evidence integrity](../multimedia-authentication/references/evidence-integrity.md).

Use the least transformative method that serves the question. Keep the source and result available side by side; label all exhibits as enhanced. Validate that a measurement survives the chosen transformation. Treat denoising, sharpening, deblurring, stabilization, interpolation, and source separation as potentially artifact-producing. Generative restoration may guide inquiry but cannot establish a recovered face, word, or other source detail without independent evidence. Follow [enhancement guidance](../multimedia-authentication/references/forensic-enhancement.md).

Report what became easier to inspect, what the source directly supports, the transformation's uncertainty, and any feature that may be algorithmic. Do not silently replace the source with the enhanced output in a report.

## Suggested workflow

Use [SWGDE *Image Processing Guidelines*, 15-M-002-1.0](https://www.swgde.org/documents/published-complete-listing/15-m-002-swgde-image-processing-guidelines/) for visual processing and [SWGDE *Best Practices for Enhancement of Digital Audio*, 20-A-001-2.0](https://www.swgde.org/documents/published-complete-listing/20-a-001-2/) for audio. Check the current versions before case use.

1. **Define the target.** State the feature or measurement to be clarified, its location, and the intended use: investigative lead, illustration, or quantitative analysis. Ask for an earlier generation if prior compression or processing limits the task. Decide in advance what observation would count as improvement and what artifacts could mislead.
2. **Assess the unprocessed source.** Preserve native bytes. Record dimensions, pixel/color properties, frame timing, or audio sample format. For image/video, inspect exposure, blur, noise, compression, interlace, motion, and color range. For audio, listen critically and inspect waveform, channels, spectrum, and spectrogram. Note variation over time or space; one setting may not suit the entire item.
3. **Plan a minimal processing chain.** Select operations for identified defects, not for cosmetic appeal. Image/video examples: orientation, deinterlace, levels, channel isolation, geometric correction, stabilization, or conservative denoise. Audio examples: de-click/de-clip, reference-channel cancellation, stationary-noise reduction, dereverberation, equalization, then gain correction where justified. The order is case-specific; test it on representative intervals or regions.
4. **Process and preserve.** Use a verified copy, save parameter files and intermediate outputs, and hash each delivered derivative. Record source coordinates/timestamps, masks, window sizes, color conversion, sample rate, bit depth, codec, and software version. Export an uncompressed or lossless working result where practicable. Do not overwrite an earlier iteration.
5. **Check for harm.** Compare processed output to source at matched coordinates and playback level. For audio, listen to the removed residual to detect target-signal loss. For images, inspect halos, ringing, false edges, interpolation, clipped values, and altered aspect ratio. Measure on the source when processing changes the property being measured. Record unsuccessful settings that materially affect interpretation.
6. **Prepare exhibits.** Label every result as enhanced, include the source and processing history, and state the narrow informational gain and residual uncertainty. A super-resolution or generative output is not an observation of detail absent from the source. An independent qualified examiner should review material conclusions drawn from enhanced exhibits.

## Suggested open source tools

| Purpose | Tool or algorithm | Consideration |
| --- | --- | --- |
| Reproducible media transforms | [FFmpeg filters](https://ffmpeg.org/ffmpeg-filters.html) | Record complete filter graph, order, stream mapping, timebase, and output codec. |
| Image operations | [OpenCV](https://docs.opencv.org/) or [scikit-image](https://scikit-image.org/docs/stable/) | Specify interpolation, kernel, border mode, channel order, and color profile. |
| Audio operations | [Audacity](https://www.audacityteam.org/), FFmpeg, Python SciPy | Record filter parameters, noise profile selection, and removed residual. |
| Playback comparison | Side-by-side source/derivative viewer and waveform/spectrogram plots | A viewer's default scaling, color management, or loudness normalization can mislead. |

Review [enhancement limits](../multimedia-authentication/references/forensic-enhancement.md) before using interpolation, denoising, or model-based restoration as evidence.
