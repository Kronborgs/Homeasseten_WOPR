# W.O.P.R wiring diagram (ESP D1 Mini + 3x MAX7219 8x32)

Denne guide viser koblingen mellem din `ESP-D1-mini-USB-c.png` controller og 3 stk. MAX7219 8x32 paneler.

> Fra ESPHome config:
>
> - `CLK = D5`
> - `MOSI = D7`
> - `CS = D8`

## Controller reference

![ESP D1 Mini USB-C](screenshots/ESP-D1-mini-USB-c.png)

## Diagram

```mermaid
flowchart LR
  PSU[5V strømforsyning] --> M1[ MAX7219 Panel 1<br/>8x32 (IN) ]
  PSU --> M2[ MAX7219 Panel 2<br/>8x32 ]
  PSU --> M3[ MAX7219 Panel 3<br/>8x32 (OUT) ]

  ESP[ESP8266 D1 Mini<br/>USB-C]

  ESP -- D7 / MOSI --> M1
  M1 -- DOUT --> M2
  M2 -- DOUT --> M3

  ESP -- D5 / CLK --> M1
  ESP -- D5 / CLK --> M2
  ESP -- D5 / CLK --> M3

  ESP -- D8 / CS(LOAD) --> M1
  ESP -- D8 / CS(LOAD) --> M2
  ESP -- D8 / CS(LOAD) --> M3

  ESP --- GND[(Fælles GND)]
  M1 --- GND
  M2 --- GND
  M3 --- GND
```

## Koblingsliste

- `ESP D5 (GPIO14)` -> `CLK` på alle 3 paneler
- `ESP D7 (GPIO13)` -> `DIN` på Panel 1
- `Panel 1 DOUT` -> `DIN` på Panel 2
- `Panel 2 DOUT` -> `DIN` på Panel 3
- `ESP D8 (GPIO15)` -> `CS/LOAD` på alle 3 paneler
- `5V` -> `VCC` på alle paneler
- `GND` (ESP + alle paneler + PSU) skal være fælles

## Vigtigt

- Start altid datakæden i den ende af første panel, der er mærket `DIN`/`IN`.
- Nogle MAX7219 boards kører fint med 3.3V logik fra ESP8266, men ved ustabil drift kan en 74HCT-level shifter forbedre signalet.