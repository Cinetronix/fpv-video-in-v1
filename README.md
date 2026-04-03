# Cinetronix FPV Video Input Board v1

KiCad hardware design for an HDMI-to-MIPI CSI bridge board, designed for FPV camera systems.

## Overview

Converts HDMI video input to MIPI CSI-2 output using the Toshiba TC9590XBG bridge IC, controlled by an ESP32-S3 microcontroller.

### Key Components

| Component | Function |
|-----------|----------|
| TC9590XBG | HDMI to MIPI CSI-2 bridge |
| ESP32-S3 | Control MCU |
| TS5MP645YFPR | HDMI multiplexer |
| TPD8S009DSMR | HDMI ESD protection |
| TPD6E05U06RVZR | Additional ESD protection |
| DF56C-26S | Micro-coax connector (CSI output) |

## Board Designs

- **TC9590XBG-PCB/** — Main board with HDMI input, CSI output, and ESP32-S3 control
- **DF56C-26S-breakout-board-PCB/** — Breakout board for the 26-pin DF56C micro-coax connector
- **DF56C-30S-breakout-board-PCB/** — Breakout board for the 30-pin DF56C micro-coax connector

## Requirements

- [KiCad](https://www.kicad.org/) 7+
- [KiKit](https://github.com/yaqwsx/KiKit) (for panel generation)

## Panelization

Generate a manufacturing panel from the `TC9590XBG-PCB/` directory:

```bash
kikit panelize \
    --layout "grid; rows: 1; cols: 3; space: 5mm;" \
    --tabs "fixed; width: 5mm;" \
    --cuts "mousebites; drill: 0.5mm; spacing: 1mm; offset: 0.2mm; prolong: 0.5mm" \
    --framing "railstb; width: 5mm; space: 3mm; mintotalheight: 72mm; mintotalwidth: 72mm" \
    --tooling "3hole; hoffset: 2.5mm; voffset: 2.5mm; size: 1.5mm" \
    --fiducials "3fid; hoffset: 5mm; voffset: 2.5mm; coppersize: 2mm; opening: 1mm;" \
    --text "simple; text: Cinetronix Video input v1.1a; anchor: mt; voffset: 2.5mm; hjustify: center; vjustify: center;" \
    --post "millradius: 1mm" \
    fpv-video-in-v1.kicad_pcb Panel/panel.kicad_pcb
```

## Project Structure

Each board subdirectory contains its own KiCad project files (`.kicad_pro`, `.kicad_sch`, `.kicad_pcb`) along with a `lib/` directory for custom symbols, footprints, and 3D models.

## License

Copyright Cinetronix. All rights reserved.
