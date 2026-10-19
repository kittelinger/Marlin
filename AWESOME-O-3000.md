# Awesome-O 3000

Umgebauter Creality Ender-3 auf Basis von Marlin `bugfix-2.1.x`.
Die Konfiguration basiert auf dem offiziellen Beispiel
`config/examples/Creality/Ender-3/BigTreeTech SKR 1.4` aus
[MarlinFirmware/Configurations](https://github.com/MarlinFirmware/Configurations).

## Hardware

| Teil | Typ |
|---|---|
| Mainboard | BigTreeTech SKR V1.4 Turbo (LPC1769) |
| Treiber | 4× TMC2209 (UART), E1-Steckplatz bestückt, aber unbenutzt |
| Display | BTT TFT35-E3 V3.0 (Touch über RS232, Marlin-Modus über EXP1/EXP2) |
| Sensoren | keine (kein Probe, kein Filamentsensor) |

## Wichtigste Einstellungen

- **Seriell:** `SERIAL_PORT 0` = TFT-Anschluss (UART0), `SERIAL_PORT_2 -1` = USB, beide 115200 Baud
- **Bauraum:** 235 × 235 × 250 mm
- **Steps/mm:** 80 / 80 / 400 / 93 (Original-Extruder)
- **Richtungen:** X, Y, E invertiert, Z normal
- **Motorströme:** X/Y/Z 580 mA, E 650 mA, StealthChop
- **PID:** Hotend und Bett (Bett-PID aktiv, Startwerte per `M303` autotunen)
- **Leveling:** manuelles Mesh Bed Leveling (3×3) und Bed Tramming über das LCD-Menü
- **EEPROM** aktiv (`M500` zum Speichern)
- **TFT-Features:** Auto-Report von Temperatur, Position und SD-Status, Host-Prompts, Emergency-Parser, `M600`, `M701/M702`, `M73`

## Build und Flashen

```
pio run -e LPC1769
```

`.pio/build/LPC1769/firmware.bin` auf die microSD-Karte des Mainboards kopieren
und den Drucker einschalten. Nach dem Flashen heißt die Datei `FIRMWARE.CUR`.
Danach `M502` und `M500` senden, damit das EEPROM die neuen Standardwerte übernimmt.

`FIRMWARE.CUR` im Repo ist eine Sicherung der alten Firmware vom Januar 2026.
