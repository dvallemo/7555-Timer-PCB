# Getting to Blinky 5.0

A two-layer PCB designed in KiCad featuring a 7555 timer astable oscillator circuit that blinks an LED. Built as a hands-on learning project to develop familiarity with KiCad's schematic capture, footprint assignment, PCB layout, and DRC workflow.

---

## Circuit Overview

The circuit uses a 555 timer (U1) configured in **astable mode** to generate a continuous square wave output that drives an LED.

| Ref | Part | Value | Description |
|-----|------|-------|-------------|
| U1 | 7555 Timer | â€” | SO-8 SMD package, custom schematic symbol |
| BT1 | CR2032 | 3V | Coin cell battery, custom PCB footprint |
| R1 | Resistor | 1kÎ© | Timing resistor (charge path) |
| R2 | Resistor | 470kÎ© | Timing resistor (discharge path) |
| R3 | Resistor | 1kÎ© | LED current limiting resistor |
| C1 | Capacitor | 1ÂµF | Timing capacitor |
| D1 | LED | â€” | Output indicator, 0805 SMD |

### How It Works

The 7555 timer alternately charges and discharges C1 through R1 and R2, producing a square wave on the OUT pin (pin 3). R3 limits current through D1. The blink frequency is set by:

```
f â‰ˆ 1.44 / ((R1 + 2Â·R2) Â· C1)
f â‰ˆ 1.44 / ((1kÎ© + 2Â·470kÎ©) Â· 1ÂµF) â‰ˆ 1.53 Hz
```

---

## PCB Details

- **Tool:** KiCad 8
- **Layers:** 2-layer board
- **Power supply:** CR2032 coin cell (3V)
- **Trace width:** 0.2mm (chosen for improved manufacturability)
- **Copper pours:** GND pour on B.Cu, VDD pour on F.Cu
- **Package sizes:** All passives in 0805 for hand solderability

### Custom Work

- **Custom schematic symbol** created for the 7555 timer (U1)
- **Custom PCB footprint** created for the CR2032 coin cell holder (BT1) using the S8211-46R footprint from the FlashLED library as a starting point

### DRC Results

| Category | Count |
|----------|-------|
| Errors | 0 |
| Warnings | 4 |
| Unconnected Items | 0 |

The 4 warnings are non-critical: 3 are single-layer via warnings resolved after copper pour fill, and 1 is a footprint-library mismatch on BT1 due to the custom footprint modification.

---

## Board Images

### Schematic
![Schematic](images/schematic.png)

### PCB Layout
![PCB Layout](images/pcb_layout.png)

### 3D Render â€” Top
![3D Top](images/3d_top.png)

### 3D Render â€” Bottom (Battery Side)
![3D Bottom](images/3d_bottom.png)

---

## Key Learnings

- KiCad schematic capture and ERC workflow
- Creating custom schematic symbols and PCB footprints
- 555 timer astable configuration and timing calculations
- Two-layer PCB layout with copper pour fills
- DRC execution and warning triage
- Silkscreen labeling and board branding

---

## Repository Structure

```
â”œâ”€â”€ Getting-to-Blinky-5.0.kicad_pro
â”œâ”€â”€ Getting-to-Blinky-5.0.kicad_sch
â”œâ”€â”€ Getting-to-Blinky-5.0.kicad_pcb
â”œâ”€â”€ symbols/
â”‚   â””â”€â”€ 7555_custom.kicad_sym
â”œâ”€â”€ footprints/
â”‚   â””â”€â”€ CR2032_custom.kicad_mod
â”œâ”€â”€ gerbers/
â””â”€â”€ images/
    â”œâ”€â”€ schematic.png
    â”œâ”€â”€ pcb_layout.png
    â”œâ”€â”€ 3d_top.png
    â””â”€â”€ 3d_bottom.png
```

---

## Author

**Dave** â€” Electrical Engineering, Stevens Institute of Technology  
PCB design portfolio project | KiCad | June 2026
