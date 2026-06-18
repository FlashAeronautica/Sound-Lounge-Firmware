# Sound Lounge — public OTA firmware

Public repository for **Sala Sound Lounge** over-the-air update binaries only.

Source code lives in the private [Sound-Lounge-Music](https://github.com/FlashAeronautica/Sound-Lounge-Music) repository. This repo is intentionally public so field units can download firmware from any network without authentication.

## Layout

| Path | Purpose |
|------|---------|
| `release/` | Production OTA channel (field units) |
| `staging/` | Test / lab OTA channel |
| `manifest.txt` | Alias to `release/manifest.txt` (legacy) |

Each channel folder contains:

- `manifest.txt` — version and download URLs
- `lounge_ui_v*.bin` — ESP32 display UI
- `lounge_player_v*.bin` — Teensy 4.1 music player
- `lounge_zones_v*.bin` — Teensy 4.0 lounge / zones

## Device manifest URLs

| Channel | URL |
|---------|-----|
| Release | https://raw.githubusercontent.com/FlashAeronautica/Sound-Lounge-Firmware/main/release/manifest.txt |
| Staging | https://raw.githubusercontent.com/FlashAeronautica/Sound-Lounge-Firmware/main/staging/manifest.txt |

## Publishing

From the private source repo:

```powershell
.\build_firmware.ps1 -Channel both
```

Then commit and push this repository (`Sound-Lounge-Firmware`).

## SD card (offline updates)

Copy a channel folder to the Box A Teensy SD card:

```
/firmware/release/manifest.txt
/firmware/release/lounge_*.bin
```

Legacy `/firmware/manifest.txt` is still supported as a release fallback.
