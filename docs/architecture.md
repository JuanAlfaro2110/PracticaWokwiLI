# Firmware Architecture

## High-Level Flow

1. `setup()` initializes serial output on `Serial1` at 115200 baud.
2. PIO program is loaded with `pio_add_program(pio0, &segment_program)`.
3. State machine is configured with `segment_program_init(...)` using:
   - first segment pin: `GP2`
   - first digit pin: `GP10`
4. `loop()` increments a counter and calls `displayNumber()` every 200 ms.

## Module/Function Breakdown

- `digits[]`:
  Lookup table for decimal digits 0-9 in 7-segment bit encoding.

- `displayNumber(uint value)`:
  Splits a numeric value into thousands/hundreds/tens/units and packs four bytes into one 32-bit word before pushing to the PIO TX FIFO.

- `setup()` / `loop()`:
  Arduino-style application lifecycle.

## Data Path

Counter (`int i`) -> `displayNumber(i++)` -> digit extraction -> 32-bit packed frame -> `pio_sm_put()` -> PIO state machine -> segment/digit GPIO lines.

## Non-Functional Notes

- Behavior intentionally unchanged from source material.
- No credential handling, storage, or networking logic is present.
