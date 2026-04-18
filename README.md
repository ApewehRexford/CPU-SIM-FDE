# CPU_SIM — Von Neumann Architecture Simulator

A web-based, interactive CPU simulator designed to visualize the Fetch-Decode-Execute (FDEC) cycle within a classic Von Neumann architecture. CPU-SIM allows users to write assembly code, load it into a unified memory space, and watch the precise flow of data across internal buses as instructions are processed.

## Features

* **Interactive FDEC Visualization:** Real-time animated data buses and visual state tracking for Fetch, Decode, and Execute phases.
* **Custom Instruction Set Architecture (ISA):** A 16-instruction set featuring arithmetic, logic, branching, and I/O operations.
* **Integrated Assembler:** Write, edit, and load custom assembly programs directly within the browser. Includes support for exporting and importing `.asm` files.
* **Execution Controls:** Step through code cycle-by-cycle, run continuously with adjustable clock speeds, or set memory breakpoints for debugging.
* **Deep State Inspection:** Live monitoring of CPU registers (PC, IR, MAR, MDR, ACC) and status flags (Zero, Negative, Carry, Overflow).
* **Configurable Memory & Base:** Supports 16, 32, or 64 cells of Unified RAM. View data in Binary, Octal, Decimal, or Hexadecimal bases.
* **Theming & UI:** Multiple color themes (Cyan, Amber, Green, Red, Paper), customizable fonts, and a retro CRT scanline effect.

## Architecture Overview

CPU-SIM implements an 8-bit architecture (4-bit opcode, 4-bit operand address) operating on a shared memory model.

### Core Registers
* **PC (Program Counter):** Holds the address of the next instruction to be fetched.
* **IR (Instruction Register):** Stores the current instruction word being decoded and executed.
* **MAR (Memory Address Register):** Holds the memory address currently being read from or written to.
* **MDR (Memory Data Register):** Buffers data transferring between the CPU and main memory.
* **ACC (Accumulator):** The primary register for ALU operations and I/O.

## Instruction Set Reference

The CPU utilizes a 4-bit opcode, allowing for 16 distinct instructions:

| Opcode (Hex) | Mnemonic | Description |
| :--- | :--- | :--- |
| `0x` | **HLT** | Halt execution. |
| `1x` | **ADD** | ACC ← ACC + MEM[x] |
| `2x` | **SUB** | ACC ← ACC - MEM[x] |
| `3x` | **STA** | MEM[x] ← ACC |
| `4x` | **LDI** | ACC ← immediate value #x |
| `5x` | **LDA** | ACC ← MEM[x] |
| `6x` | **JMP** | Unconditional jump to address x (PC ← x) |
| `7x` | **JZ** | Jump to x if Zero (Z) flag is set |
| `8x` | **OUT** | Output ACC value to the I/O log |
| `9x` | **INP** | Pause execution and wait for user input into ACC |
| `Ax` | **AND** | ACC ← ACC & MEM[x] (Bitwise AND) |
| `Bx` | **OR** | ACC ← ACC \| MEM[x] (Bitwise OR) |
| `Cx` | **MUL** | ACC ← ACC × MEM[x] |
| `Dx` | **JNZ** | Jump to x if Zero (Z) flag is clear |
| `Ex` | **NOP** | No operation |
| `Fx` | **NOT** | ACC ← ~ACC (Bitwise NOT) |

*Note: `x` represents the 4-bit operand address or immediate value.*

## Getting Started

Because CPU_SIM is built entirely with client-side web technologies (HTML, CSS, JS), there is no build process or dependency installation required.

1.  Clone the repository:
    ```bash
    git clone https://github.com/yourusername/rex-sim.git
    ```
2.  Open the directory and double-click `CPU_SIM.html` (or serve it via a local web server) to launch the simulator in any modern web browser.

## Basic Usage

1.  **Write Code:** Enter your assembly program in the "PROGRAM EDITOR" panel on the left.
2.  **Load:** Click the **▼ LOAD TO MEMORY** button to assemble and write your program to RAM.
3.  **Execute:** Use the **► STEP** button to advance the clock cycle manually, or **▶▶ RUN** to execute automatically based on the speed slider.
4.  **Interact:** If your code uses the `INP` instruction, the simulator will pause. Type a number into the Input Queue and press `Enter` to resume.
5.  **Debug:** Click any memory address in the UNIFIED MEMORY table to toggle a breakpoint.
