# Supplementary C2PA metadata reader

`meta3.py` is an unchanged copy of [robertoamoreno/C2PAC `meta3.py`](https://raw.githubusercontent.com/robertoamoreno/C2PAC/refs/heads/main/meta3.py), retrieved 16 October 2026 (SHA-256 `798e2d5769bf8fd4a8bf95b42fb504195aa264406184db17b4d69da5baad06f0`). The upstream repository does not declare a license as of that date; resolve redistribution rights before publishing a release that includes this copy.

Requires Python and ExifTool on `PATH`. Use only the read path:

```sh
python image-authentication/tools/meta3.py path/to/image.jpg
```

The script wraps `exiftool -json` and prints its metadata. It does **not** detect every C2PA manifest, validate signatures, check content binding or certificate trust, or identify generated imagery on its own. Its `--extract-binary` option is a placeholder; `--remove` makes a metadata-stripped derivative. Use [c2patool](https://github.com/contentauth/c2patool/blob/main/docs/usage.md) on preserved bytes for C2PA verification and follow the [image authentication C2PA check](../SKILL.md#c2pa-check-for-images).
