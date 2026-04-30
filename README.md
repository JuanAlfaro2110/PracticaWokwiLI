# Raspberry Pi Pico W - 4-Digit 7-Segment (PIO) Demo

This repository documents and organizes a Wokwi simulation project that uses a Raspberry Pi Pico/Pico W to drive a 4-digit 7-segment display through GPIO multiplexing and a PIO helper program.

> Scope note: the core firmware logic has been preserved exactly as provided and moved into a clean `src/` layout.

## Repository Structure

- `src/main.cpp` - Main firmware (Arduino-style `setup()`/`loop()` using PIO API helper header).
- `include/` - Reserved for project headers.
- `docs/wiring.md` - Wiring and GPIO mapping.
- `docs/architecture.md` - Code/module architecture and runtime behavior.
- `diagram.json` - Wokwi hardware topology.
- `CMakeLists.txt` - Project root build metadata placeholder for C/C++ structure.

## Features

- Counts up continuously and displays values on a 4-digit 7-segment module.
- Uses packed 32-bit writes to update all digits in one `pio_sm_put()` transaction.
- Uses Pico UART pins (`GP0`/`GP1`) for serial monitor routing in Wokwi.

## Components List

Derived from `diagram.json`:

1. Raspberry Pi Pico / Pico W board (`wokwi-pi-pico`)
2. 4-digit 7-segment display (`wokwi-7segment`, `digits=4`)
3. Wokwi Serial Monitor virtual endpoint

## Quick Start (Wokwi)

1. Open Wokwi and create/import a Raspberry Pi Pico project.
2. Paste `diagram.json` into the project diagram.
3. Use `src/main.cpp` as firmware source and ensure `segment.pio.h` is available in the project.
4. Start simulation.
5. Open Serial Monitor to view the startup line:
   - `Raspberry Pi Pico PIO 7-Segment Example`

## Run on Real Hardware (Pico W)

1. Use Raspberry Pi Pico SDK or Arduino-Pico environment with PIO support.
2. Copy `src/main.cpp` and required PIO header/source (`segment.pio.h`) into your firmware project.
3. Build and flash UF2 to the Pico W.
4. Wire exactly as documented in `docs/wiring.md`.

## Wi-Fi Notes

This project does **not** use Wi-Fi features. No credentials are required or stored.

## Assumptions

- The active firmware for this diagram is the 7-segment PIO example.
- A second keypad/LED sketch provided in the prompt is treated as alternate sample input and is intentionally not activated, since it does not match the provided diagram wiring.
