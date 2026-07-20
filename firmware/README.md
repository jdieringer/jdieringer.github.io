# Firmware assets

Each subfolder is one flashable build, surfaced on [`/flash.html`](../flash.html) via
[ESP Web Tools](https://esphome.github.io/esp-web-tools/) (browser flashing over Web Serial).

```
firmware/
└── angle-gauge/    F3A Setup Tools — Angle Gauge (M5StickS3 / ESP32-S3, 8 MB)
    ├── manifest.json
    └── rig-full-8MB.bin   bootloader + partitions + app + LittleFS console → 0x0
```

`rig-full-8MB.bin` is the complete image — one file, flashed at offset `0x0`, no separate
filesystem upload.

## Updating

Rebuild the bundle in the Inclinometer repo, then copy both files across:

```bash
../Inclinometer/scripts/make_bundle.sh          # produces dist/rig-full-8MB.bin
cp ../Inclinometer/dist/rig-full-8MB.bin firmware/angle-gauge/
cp ../Inclinometer/dist/manifest.json    firmware/angle-gauge/
```

Bump `version` in `manifest.json`, commit, and push.

## Notes

- `new_install_prompt_erase` is `false`, so NVS survives a reflash — a node keeps its role,
  zero, and thresholds. Set it `true` for a truly clean install.
- Target is an 8 MB ESP32-S3; the partition offsets are baked into the merged image.
- Web Serial needs a Chromium-based desktop browser over **HTTPS** (GitHub Pages qualifies) or
  `localhost`. It does not work from a `file://` page.
- To add a build: create a folder with a `manifest.json` and add an entry to the `FIRMWARE`
  list in `flash.html`.
