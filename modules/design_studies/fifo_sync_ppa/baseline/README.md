# Baseline FIFO – PPA Study

Target Device: Artix-7 (xc7a35t)  
Clock Constraint: 100 MHz (10 ns)

---

## 1. Area Report (Post-Implementation)

- CLB LUTs: 62  
- Registers (FFs): 149  
- Block RAM: 0  
- BUFG: 1  

### Observations

- FIFO storage (16 × 8 = 128 bits) is implemented using flip-flops.
- No BRAM inferred due to small memory depth.
- Register usage is dominated by memory storage and counter logic.
- Area footprint is very small.

---

## 2. Timing Report (Post-Implementation)

Clock Period Constraint: 10 ns (100 MHz)

- Worst Negative Slack (WNS): +6.056 ns  
- Estimated Critical Path Delay: ~3.94 ns  
- Estimated Fmax: ~253 MHz  

### Critical Path

From:
- `count_reg[1]`

To:
- `mem_reg[3][0]/CE`

Critical path is in control logic (counter → memory enable).

### Delay Breakdown

- Logic Delay: ~20%
- Routing Delay: ~80%

Routing dominates timing, which is typical in FPGA designs.

---

## 3. Power Report (Post-Implementation)

- Total On-Chip Power: (from report)
- Dynamic Power: (from report)
- Static Power: (from report)

### Observations

- Power consumption is low due to small design size.
- Dynamic power primarily due to clock and memory toggling.
- No clock gating or power optimization applied.

---

## Baseline Summary

The baseline FIFO:

- Meets 100 MHz timing comfortably.
- Has significant timing margin (~6 ns slack).
- Uses distributed registers instead of BRAM.
- Is control-path limited rather than memory limited.

This baseline will be used for comparison against:

- Area-optimized version
- Performance-optimized version
- Power-optimized version