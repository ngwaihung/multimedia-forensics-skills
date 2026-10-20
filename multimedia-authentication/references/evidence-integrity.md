# Evidence integrity and examination protocol

## Intake record

For each item, record case identifier, unique item identifier, filename (including extension), original path or source URI, acquisition method, supplied-by, received-by, receipt time with timezone, byte count, SHA-256, and whether it is an original, export, copy, or unknown. Record packaging and any pre-existing damage or missing segments. A filename, extension, and filesystem timestamp are descriptive, not proof of origin.

If acquisition is under examiner control, document device/application, settings, clock state, transfer route, and any unavoidable changes. Avoid opening evidence in software that may update metadata before making a verified copy. For remote or cloud material, record the exact download method, URL or object identifier, headers and platform metadata when available, and whether the platform transformed the media.

## Custody and derivatives

Maintain an append-only examination log: time with timezone, actor, action, input item/hash, tool and version, exact command or settings, output item/hash, and result. Record access and custody transfers separately. Hash immediately after intake and after each copy; compare hashes before analysis. A hash establishes byte identity at those times, not truthfulness or original provenance.

Keep source bytes read-only when feasible. Do analysis on a verified working copy. Give every extracted frame, demuxed stream, cropped region, normalized audio file, visualization, and enhanced output a unique identifier linked to its parent and parameters. Preserve native timebase, sample rate, dimensions, color metadata, and time mapping when deriving material; record changes and avoid relying on a player screenshot for measurements.

For any comparison across files, confirm whether files are byte-identical, visually identical after re-encoding, or genuinely independent acquisitions. Shared ancestry weakens corroboration. Track timezones, clock drift, and file-system granularity when interpreting times.

## Decision points

If hashing or copying fails, stop processing that item and document the failure. If a parser reports damage, retain the bytes and capture its errors; do not silently repair the source. If preservation cannot be established for material already received, state the specific gap and restrict conclusions that depend on pre-receipt integrity. Do not invent custody history.
