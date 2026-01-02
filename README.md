# Asynchronous Bidirectional Handshaking System Using Polling on Dual DMC8 Processors (DEEDS)

## Overview
This project implements an **asynchronous parallel data exchange** between two **DMC8 microprocessors** (Manager and Worker) using:
- **Polling**
- **Bidirectional Handshaking** (STB/ACK, four-phase protocol)

The **Manager** reads an 8-bit value from input switches, places it on a shared data bus, and initiates transfer.  
The **Worker** waits for the strobe, captures the data, displays it on LEDs, and acknowledges receipt.

---

## Files Included
- `ManagerWorker.pbs`: DEEDS circuit containing both DMC8 CPUs and wiring
- `manager.asm`: Manager CPU assembly program
- `worker.asm`: Worker CPU assembly program
- `Report.pdf`: 2 page project report

---

## Requirements
- **DEEDS Digital Circuit Simulator** (downloaded from: https://www.digitalelectronicsdeeds.com)
- The **DMC8** processor module (included inside DEEDS)

---

## How to Run (Step-by-Step)

### 1) Open the circuit
1. Launch **DEEDS**.
2. Go to **File → Open**.
3. Select and open the circuit file: `ManagerWorker.pbs`.

You should see two DMC8 CPUs labeled **MANAGER** and **WORKER**, input switches on the Manager side, and LED output on the Worker side.

---

### 2) Load the Manager program
1. Click on the **MANAGER** DMC8 CPU.
2. Open its program editor/assembler (commonly: **Assembler**, **Edit Program**, or **ROM/Program** option).
3. Load the file `manager.asm`.
4. Assemble/compile the program.
5. Ensure it is loaded into the Manager’s ROM.

---

### 3) Load the Worker program
1. Click on the **WORKER** DMC8 CPU.
2. Open its program editor/assembler.
3. Load the file `worker.asm`.
4. Assemble/compile the program.
5. Ensure it is loaded into the Worker’s ROM.

---

### 4) Start the simulation
1. Set the simulation clock to a visible rate (recommended **50 Hz** for demo).
2. Click **Run** (Play button).

---

## How to Test the System

### Test A: Normal transfer
1. Toggle any combination of the 8 input switches connected to the Manager’s input (IA).
2. The Worker should capture the value and show it on its LEDs (OA output).

**Expected behavior**
- Data appears on Worker LEDs only when the handshake completes.
- Transfers repeat continuously as you change switch values.

---

### Test B: Handshake signal behavior (optional observation)
- **STB (strobe)** is driven by the Manager to indicate “data valid”.
- **ACK (acknowledge)** is driven by the Worker to indicate “data received”.

**Expected sequence**
1. Manager outputs data → sets **STB = 1**
2. Worker reads data → sets **ACK = 1**
3. Manager clears **STB = 0**
4. Worker clears **ACK = 0**

---

## Notes / Troubleshooting

### Worker LEDs do not change
- Confirm both programs were assembled successfully with **no errors**.
- Confirm the Manager’s output bus is wired to the Worker’s input.
- Confirm STB/ACK wires are connected to the correct ports/bits:
  - STB: Manager → Worker (control line)
  - ACK: Worker → Manager (control line)

### Simulation runs too fast
- Reduce clock speed (e.g., 10–50 Hz) to observe control transitions.

---

## Author / Course
- Course: Digital Systems / Chapter 4 (DEEDS, DMC8 Assembly)
- Technique used: Polling + Bidirectional Handshaking
