# W.O.P.R Rack Display (ESPHome + Home Assistant)

Custom W.O.P.R-inspired rack display built with **ESP8266 (D1 Mini)**, **MAX7219 96x8 LED matrix**, **ESPHome**, and **Home Assistant**.

This project combines live network data from **UniFi** with status data from **Unraid Management Agent** in a DEFCON-inspired dashboard.

## Credits

- 3D-print rack-mount STL design: MakerWorld model by the original creator
  https://makerworld.com/en/models/1670433-rack-mounted-led-matrix-8x96-wopr-style?from=search#profileId-1768436

## What This Project Does

- Displays a dynamic W.O.P.R matrix on a physical 96x8 LED panel
- Matrix activity reacts to:
  - Number of online clients (UniFi)
  - WAN traffic/load (UniFi RX + TX)
- Includes intro sequence: **"MY NAME IS JOSHUA, SHALL WE PLAY A GAME?"**
- Exposes live matrix rows to Home Assistant as text sensors
- Provides controls directly in Home Assistant:
  - Brightness
  - Effect Intensity
  - Fill Override
  - Replay Intro
- Includes a complete Home Assistant dashboard with:
  - WOPR Live Matrix (emoji-rendered)
  - WOPR Controls
  - Unraid server/array/parity/status views
  - Performance gauges (CPU, RAM, temperature, etc.)

## Demo & Images

Place your media files in `docs/screenshots/` using these exact filenames:

- `WOPR.gif` (Home Assistant demo)
- `01-dashboard-overview.png` (dashboard overview)
- `ESP-D1-mini-USB-c.png` (controller reference)
- `physical-rack-display.jpg` (photo of the real display)

### Home Assistant demo (GIF)
![WOPR Home Assistant Demo](docs/screenshots/WOPR.gif)

### Dashboard overview
![Dashboard Overview](docs/screenshots/01-dashboard-overview.png)

### ESP D1 Mini controller
![ESP D1 Mini USB-C](docs/screenshots/ESP-D1-mini-USB-c.png)

### Physical rack display
![Physical Rack Display](docs/screenshots/physical-rack-display.jpg)

## Hardware

- 1x ESP8266 D1 Mini
- 12x MAX7219 modules (daisy-chained) = 96x8 matrix
- Power supply sized for matrix + ESP

## Shopping List (Beyond Filament)

- 3x MAX7219 8x32 (4-in-1) dot matrix modules
  https://www.amazon.de/dp/B07HJDV3HN?th=1
- Screw/nut assortment (M3/M4/M5/M6)
  https://www.amazon.de/dp/B0DQ16QCRW?th=1
- ESP32 Mini USB-C dev boards (3-pack)
  https://www.amazon.de/-/en/gp/product/B0D7V9591B?smid=AACU6YN8E2OJC&th=1

### You Will Also Typically Need

- 5V power supply with enough current for the full matrix (with margin)
- Signal wires/jumper wires (Dupont)
- Power wires for 5V/GND distribution across all panels
- Optional DC barrel connector or screw terminals for clean power input
- Soldering iron + solder (if modules/connections need permanent wiring)
- Heat shrink / cable ties for rack cable management

### Important Board-Type Note

- This repo is configured for `ESP8266 D1 Mini` in ESPHome.
- If you use the ESP32 board from the link, update the board/platform in ESPHome accordingly.

## Files in This Repo

- `ESPhome_WOPR.yaml` – ESPHome configuration for the WOPR display
- `WOPR_Dashboard_HA.yaml` – Home Assistant Lovelace dashboard configuration
- `docs/WIRING_DIAGRAM.md` – wiring diagram for ESP D1 Mini + 3x MAX7219 8x32

## Prerequisites

- Home Assistant
- ESPHome integration i Home Assistant
- UniFi integration in Home Assistant (client and WAN sensors)
- Unraid Management Agent integration (server/dashboard data)

## Quick Setup

1. Copy `ESPhome_WOPR.yaml` into your ESPHome configuration.
2. Make sure `secrets.yaml` contains:
   - `wifi_ssid`
   - `wifi_password`
3. Adjust entity IDs in `ESPhome_WOPR.yaml` if your UniFi sensors use different names.
4. Flash your D1 Mini using ESPHome.
5. Import/paste `WOPR_Dashboard_HA.yaml` into your Home Assistant Lovelace dashboard.
6. Update dashboard entity IDs as needed for your environment.

## Pinout (from ESPHome config)

- CLK: `D5`
- MOSI: `D7`
- CS: `D8`

## Wiring diagram

See the full wiring guide here:

- [docs/WIRING_DIAGRAM.md](docs/WIRING_DIAGRAM.md)

## Notes

- This repo is intended as a project reference and may require minor sensor-name adjustments in other HA environments.
- The configuration is intentionally kept close to the currently running setup.

## Roadmap (Ideas)

- More visual modes (for example alarm/idle)
- Automatic fallback when UniFi data is unavailable
- Optional MQTT mirror of matrix state

---

If you want, I can also add a **LICENSE suggestion** and a ready-to-use **GitHub release text**.
