# Maintainer notes — Sound-Lounge-Firmware

Customer-facing instructions live in [README.md](README.md). This file is for repository layout, publishing, and migration planning.

Build and publish workflow detail remains in the private **Sound-Lounge-Music** repo: `docs/NEXT_FIRMWARE.md`.

---

## Target layout (migration in progress)

**Current state (0.15.04+):** packages are dual-published to the **repo root** and `next/` so older players (`.../main/next`) and new players (`.../main`) both work.

**Target state** when approved:

```
Sound-Lounge-Firmware/
  README.md
  MAINTAINERS.md
  manifest.txt
  music_player_ui_<ver>.bin
  music_player_sound_<ver>.bin
  sound_lounge_<ver>.bin
```

**Remove when approved:** `next/`, `staging/`, `release/`, legacy root manifest format, old `.bin` files.

`build_firmware_next.ps1` copies each build to both repo root and `next/` automatically when `../Sound-Lounge-Firmware` exists.

Firmware **0.15.04+** uses `GITHUB_FW_BASE_URL` → repo root with fallback to `.../main/next`.

---

## Publishing checklist (dual-publish — root + `next/`)

Until `next/` is removed:

1. Bump **`FIRMWARE_VERSION` to the same value** in all three `*_Next/Config.h` files.
2. `.\build_firmware_next.ps1 -Summary "Next OTA x.y.zz: …"` (auto-copies to `Sound-Lounge-Firmware` root and `next/` when sibling repo exists).
3. Update **Current firmware version** in [README.md](README.md).
4. Remove obsolete `.bin` files from repo root and `next/` before commit.
5. Commit and push `Sound-Lounge-Firmware` to `main`.

All three component versions in `manifest.txt` must match top-level `version=`.

---

## Customer README policy

[README.md](README.md) must stay **operator-focused**:

- How to use **Upgrade Online** and **Upgrade Local** on the device.
- How to download and copy a package to the SD card `firmware` folder.
- Safety notes (power, do not remove SD mid-update).

Do **not** include in the public README: MCU types, manifest key names, install order, publish workflows, staging/release channel matrix, or links to private source repos.
