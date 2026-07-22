# Firmware assets

Flashable builds are surfaced on [`/flash.html`](../flash.html) via
[ESP Web Tools](https://esphome.github.io/esp-web-tools/) (browser flashing over Web Serial).

Builds are **sourced from their project repos**, not stored here — the flasher points each
build's `manifest` at a raw URL, so the firmware repo stays the single source of truth and this
site carries no multi-MB binaries.

```
angle-gauge   F3A Setup Tools — Angle Gauge (M5StickS3 / ESP32-S3, 8 MB)
              manifest: https://raw.githubusercontent.com/jdieringer/f3a-angle-gauge/main/dist/manifest.json
              bin:      dist/rig-full-8MB.bin  (bootloader + partitions + app + LittleFS console → 0x0)
```

`rig-full-8MB.bin` is the complete image — one file, flashed at offset `0x0`, no separate
filesystem upload.

## Updating

Nothing to copy here. Rebuild and push in the firmware repo:

```bash
scripts/make_bundle.sh   # in jdieringer/f3a-angle-gauge → produces dist/rig-full-8MB.bin + manifest.json
```

Bump `version` in that repo's `dist/manifest.json`, commit, and push to `main`. `flash.html`
picks it up automatically on the next load. (The raw URL is pinned to the `main` branch, so
whatever is on `main` is what gets flashed.)

## Notes

- `new_install_prompt_erase` is `false`, so NVS survives a reflash — a node keeps its role,
  zero, and thresholds. Set it `true` for a truly clean install.
- Target is an 8 MB ESP32-S3; the partition offsets are baked into the merged image.
- `raw.githubusercontent.com` serves the bin with `Access-Control-Allow-Origin: *`, so the
  cross-origin fetch from the flasher works without a proxy.
- Web Serial needs a Chromium-based desktop browser over **HTTPS** (GitHub Pages qualifies) or
  `localhost`. It does not work from a `file://` page.
- To add a build: add an entry to the `FIRMWARE` list in `flash.html` with a `manifest` URL
  (raw repo URL or a local path).
