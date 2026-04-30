# Wiring and GPIO Mapping

## Overview

The wiring corresponds to a multiplexed 4-digit 7-segment display connected directly to Raspberry Pi Pico GPIO lines.

## Components

- 1x Raspberry Pi Pico / Pico W
- 1x 4-digit 7-segment display

## GPIO Mapping Table

| Pico Pin | Signal | Display Pin | Purpose |
|---|---|---|---|
| GP0 | UART0 TX | Serial Monitor RX | Debug output |
| GP1 | UART0 RX | Serial Monitor TX | Debug input |
| GP2 | SEG_A | A | Segment A control |
| GP3 | SEG_B | B | Segment B control |
| GP4 | SEG_C | C | Segment C control |
| GP5 | SEG_D | D | Segment D control |
| GP6 | SEG_E | E | Segment E control |
| GP7 | SEG_F | F | Segment F control |
| GP8 | SEG_G | G | Segment G control |
| GP9 | SEG_DP | DP | Decimal point control |
| GP10 | DIGIT_1 | DIG1 | Digit select 1 |
| GP11 | DIGIT_2 | DIG2 | Digit select 2 |
| GP12 | DIGIT_3 | DIG3 | Digit select 3 |
| GP13 | DIGIT_4 | DIG4 | Digit select 4 |

## Multiplexing Behavior

The firmware writes packed segment states for all four digits through a PIO state machine. Digit enable lines (GP10-GP13) select active digit positions rapidly enough to appear continuously lit.

## Real Hardware Notes

- Keep a common ground between Pico W and display driver circuitry.
- If using a bare display module (not simulation component), add proper current limiting and transistor/driver stages as required by your display type (common anode/cathode).
