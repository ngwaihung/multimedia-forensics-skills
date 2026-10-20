# Audio splicing examination

**Question:** Was a specified interval removed, inserted, reordered, or otherwise joined? Record the alleged location and the smallest relevant time window.

1. Preserve encoded bytes and identify capture/export generation, codec, channels, sample rate, and timing. Demux without transcoding if possible; log any decoding.
2. Listen to the source at normal speed and annotate candidate boundaries. Inspect encoded frame continuity, waveform, spectrogram, channel phase, noise floor, reverberation, and ambient sound around each boundary.
3. Test splice and benign hypotheses, including voice activity detection, automatic gain, denoising, packet loss, microphone movement, and acoustic scene changes. Compare control intervals from the same recording or device when available.
4. Seek independent corroboration from video, an earlier recording, transcript chronology, or a different acoustic/structural signal. Treat enhanced or separated audio as an investigative derivative.
5. Report boundary times with uncertainty and the source timebase, observed features, rival explanations, processing parameters, and the extent to which a splice is supported or cannot be determined.

See [audio authentication](../references/audio-authentication.md) and [evidence integrity](../references/evidence-integrity.md).
