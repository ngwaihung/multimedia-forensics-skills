# File structure and metadata

## Sequence

1. Confirm byte signature, actual format, size, and whether the file is complete. Compare extension, MIME inference, parser output, and raw header where a mismatch matters.
2. Record metadata with namespaced tags and raw values where possible: EXIF, XMP, IPTC, maker notes, QuickTime/ISO BMFF, ID3/BWF, filesystem attributes, and sidecars. Preserve embedded thumbnails and previews as separate evidence of processing history, not as ground truth.
3. Parse container and streams: tracks, codecs, profiles, dimensions, frame/sample rates, timebases, duration, start times, rotation, color primaries/transfer/range, audio layout, bitrate, and encoder tags. Inspect MP4/MOV box order and relevant `moov`, `mdat`, track, sample table, edit list, metadata, and fragmented boxes when the question needs it. Matroska and other formats require their own structure.
4. Compare internal timestamps and counters, stream durations, file-system times, and asserted capture chronology. Convert timezones explicitly; distinguish creation, modification, encoding, export, and download events. Flag a discrepancy only after considering clock error, timezone, metadata rewriting, and normal software behavior.
5. Investigate encoding history through structural evidence, quantization/compression characteristics, encoder strings, and comparison exports. Metadata can be forged, stripped, or rewritten; encoder identification is usually limited to a software family or processing step, not an individual actor.

Use ExifTool for broad tag extraction, MediaInfo for stream summaries, and FFprobe for stream, packet, and frame timing. Capture command lines, versions, warnings, and output. For a contested box or tag, confirm offsets and interpretation with a second parser or documented byte inspection. Never treat a single tag as independent corroboration of another tag written by the same exporter.

Potentially useful commands, adapted to file and environment:

```text
exiftool -G1 -a -s -u input.ext
mediainfo --Full input.ext
ffprobe -v warning -show_format -show_streams -of json input.ext
ffprobe -v warning -select_streams v:0 -show_packets -show_entries packet=pts_time,dts_time,duration_time,flags,pos -of csv input.ext
```

Outputs can be large; preserve full logs as artifacts and cite relevant excerpts with item and byte/time offsets in findings. For protected or sealed data, use the approved examination environment and log any decryption or repair step.
