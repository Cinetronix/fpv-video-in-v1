# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

KiCad hardware design project for the Cinetronix FPV video input board (v1). Converts HDMI video input to MIPI CSI output using the Toshiba TC9590XBG bridge IC, controlled by an ESP32-S3.

## Board Designs

- **TC9590XBG-PCB/** — Main board. Key ICs: TC9590XBG (HDMI-to-CSI bridge), ESP32-S3 (control MCU), TS5MP645YFPR (HDMI mux), TPD8S009DSMR & TPD6E05U06RVZR (ESD protection). Uses DF56C-26S micro-coax connector for CSI output.
- **DF56C-26S-breakout-board-PCB/** — Breakout board for the 26-pin DF56C connector.
- **DF56C-30S-breakout-board-PCB/** — Breakout board for the 30-pin DF56C connector.

## Net Classes (Main Board)

Three net classes with specific routing constraints defined in the project file:
- **Default** — 0.09mm track, 0.127mm clearance
- **HDMI** (`/HDMI_*`) — 0.127mm track, 0.1mm clearance, 0.125mm diff pair width
- **CSI** (`/CSI_*`) — 0.09mm track, 0.127mm clearance

## Panelization

The main board uses [KiKit](https://github.com/yaqwsx/KiKit) for panel generation:

```bash
# From TC9590XBG-PCB/ directory (Windows .bat, adapt for macOS):
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

## Component Libraries

Each board has a `lib/` directory with custom symbol/footprint/3D model libraries. Symbol and footprint tables are per-project (`sym-lib-table`, `fp-lib-table`).

## KiCad Notes

- KiCad 7+ project format (`.kicad_pro`, `.kicad_sch`, `.kicad_pcb`)
- Backup/autosave files are gitignored; exported manufacturing files (gerbers, BOM CSVs, panels) are also gitignored
- The `build/` directory is gitignored — use it for any generated output
