# BIT151 Microprocessor and Computer Architecture: Exam-Ready Answers

Written for the TU BIT 2nd semester paper. Topics are ordered by how often they repeat in 2078-2082 and the model question.

**How to use this:** Learn the answers, then rewrite them by hand from memory. Do not just read them. Programs and numericals especially must be practiced on paper.

**Check before the exam:** These are written from standard textbook content (Mano, Gaonkar, Malvino). Diagrams are simplified ASCII; redraw them neatly in the exam with labels. Cross-check anything you're unsure of against your class notes.

## Contents

1. [Pipelining](#1-pipelining)
2. [8085 Assembly Programs](#2-8085-assembly-programs)
3. [Memory Hierarchy](#3-memory-hierarchy)
4. [Isolated I/O vs Memory-Mapped I/O](#4-isolated-io-vs-memory-mapped-io)
5. [SAP-1 and SAP-2](#5-sap-1-and-sap-2)
6. [Flags in 8085](#6-flags-in-8085)
7. [RISC vs CISC](#7-risc-vs-cisc)
8. [Control Unit and Microprogramming](#8-control-unit-and-microprogramming)
9. [Arithmetic Micro-operations](#9-arithmetic-micro-operations)
10. [8085 Architecture](#10-8085-architecture)
11. [Addressing Modes and 8085 Instructions](#11-addressing-modes-and-8085-instructions)
12. [Booth Multiplication](#12-booth-multiplication)
13. [Restoring Division](#13-restoring-division)
14. [DMA](#14-dma)
15. [Virtual Memory and Page Replacement](#15-virtual-memory-and-page-replacement)
16. [Number Representation and Complements](#16-number-representation-and-complements)
17. [Quick Hits](#17-quick-hits)

---

## 1. Pipelining

### Definition

Pipelining is a technique where a task is divided into sub-operations (segments), and each segment is executed in a dedicated stage. Different stages work on different tasks at the same time, like an assembly line. It increases **throughput**, not the time taken by a single task.

### Role in computing

- Overlaps execution of multiple instructions or operations.
- Raises throughput without raising clock speed dramatically.
- Used in instruction execution (CPU), arithmetic units (floating-point), and vector processors.

### Speedup ratio

For `k` segments, `n` tasks, clock period `tp`, and non-pipelined time per task `tn`:

```
Speedup S = (n * tn) / ((k + n - 1) * tp)
As n -> infinity, S -> tn / tp  (about k when tn = k * tp)
```

**Example:** k = 4, tp = 20 ns, tn = 80 ns, n = 100 tasks.
S = (100 x 80) / ((4 + 99) x 20) = 8000 / 2060 = **3.88**, close to the maximum of 4.

### Instruction pipeline

An instruction pipeline overlaps the phases of consecutive instructions, so while one instruction executes, the next is being decoded and another is being fetched.

### Four-segment instruction pipeline

| Segment | Name                               | Function                                                   |
| ------- | ---------------------------------- | ---------------------------------------------------------- |
| 1       | **FI** (Fetch Instruction)         | Fetch the instruction from memory                          |
| 2       | **DA** (Decode, calculate Address) | Decode the instruction and calculate the effective address |
| 3       | **FO** (Fetch Operand)             | Fetch the operand from memory                              |
| 4       | **EX** (Execute)                   | Execute the instruction and store the result               |

Space-time diagram:

```
Clock:  1    2    3    4    5    6    7
I1      FI   DA   FO   EX
I2           FI   DA   FO   EX
I3                FI   DA   FO   EX
I4                     FI   DA   FO   EX
```

Four instructions finish in 7 clocks instead of 16.

**Branch problem:** If instruction I2 is a branch, the pipeline must be flushed and the target fetched. The instructions already fetched behind it are wasted, which costs cycles.

### Arithmetic pipeline (floating-point add/subtract)

Example operands: X = 0.9504 x 10^3 and Y = 0.8200 x 10^2.

| Segment | Operation              | Example                                          |
| ------- | ---------------------- | ------------------------------------------------ |
| 1       | Compare exponents      | Difference = 3 - 2 = 1, so shift the smaller one |
| 2       | Align mantissas        | Y = 0.0820 x 10^3                                |
| 3       | Add/subtract mantissas | Z = 1.0324 x 10^3                                |
| 4       | Normalize the result   | Z = 0.10324 x 10^4                               |

Each segment has registers between stages, so a new pair of operands enters every clock.

### Pipeline hazards and solutions

| Hazard                   | Cause                                                                   | Solution                                                                               |
| ------------------------ | ----------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| **Structural**           | Two instructions need the same hardware at once (e.g., one memory port) | Duplicate resources, separate instruction/data memory                                  |
| **Data** (RAW, WAR, WAW) | An instruction needs a result that a previous one hasn't produced yet   | Operand forwarding, hardware interlock (stall), compiler reordering/NOPs, delayed load |
| **Control** (branch)     | A branch changes the PC, so fetched instructions are wrong              | Prefetch both paths, branch prediction, branch target buffer, delayed branch           |

### Flynn's classification

Based on the number of instruction streams and data streams:

| Type     | Instruction stream | Data stream | Example                               |
| -------- | ------------------ | ----------- | ------------------------------------- |
| **SISD** | Single             | Single      | Classic uniprocessor                  |
| **SIMD** | Single             | Multiple    | Vector/array processors, GPUs         |
| **MISD** | Multiple           | Single      | Rare; fault-tolerant/systolic designs |
| **MIMD** | Multiple           | Multiple    | Multiprocessors, multicore systems    |

### Performance of a pipelined processor (short note)

Ideal speedup is limited to the number of stages `k`. Real speedup is lower because of hazards (stalls), branch penalties, unequal stage delays (the slowest stage sets the clock), and register overhead between stages. Throughput approaches one instruction per clock for long, hazard-free streams.

---

## 2. 8085 Assembly Programs

These appear on **every** paper. Memorize the logic, not just the code. Always end with `HLT`.

### a) Add two numbers at 2030H and 2040H, store the sum at 2050H

```asm
        LDA 2030H      ; A = first number
        MOV B, A       ; B = first number
        LDA 2040H      ; A = second number
        ADD B          ; A = A + B
        STA 2050H      ; store the sum
        HLT
```

For a carry, add `MVI C,00H` at the start, `JNC SKIP`, `INR C`, `SKIP:` after `ADD B`, and store C at 2051H.

### b) Swap the contents of 8000H and 9000H

```asm
        LDA 8000H      ; A = [8000H]
        MOV B, A       ; B = [8000H]
        LDA 9000H      ; A = [9000H]
        STA 8000H      ; [8000H] = old [9000H]
        MOV A, B
        STA 9000H      ; [9000H] = old [8000H]
        HLT
```

### c) Multiply 08H x 09H (repeated addition), product at 8050H, carry at 8051H

```asm
        MVI B, 09H     ; B = multiplier (counter)
        MVI C, 08H     ; C = multiplicand
        MVI A, 00H     ; A = product (low byte)
        MVI D, 00H     ; D = product (high byte / carry)
LOOP:   ADD C          ; A = A + C
        JNC SKIP
        INR D          ; carry occurred, so increment high byte
SKIP:   DCR B
        JNZ LOOP
        STA 8050H      ; low byte
        MOV A, D
        STA 8051H      ; carry / high byte
        HLT
```

Result: 08 x 09 = 72 = 48H, so 8050H = 48H and 8051H = 00H.

### d) Divide two 8-bit numbers (repeated subtraction)

Dividend at 2000H, divisor at 2001H. Quotient goes to 2002H and remainder to 2003H.

```asm
        LDA 2001H
        MOV C, A       ; C = divisor
        LDA 2000H      ; A = dividend
        MVI D, 00H     ; D = quotient
LOOP:   CMP C          ; compare A with C (carry set if A < C)
        JC DONE        ; if A < divisor, stop
        SUB C          ; A = A - C
        INR D          ; quotient++
        JMP LOOP
DONE:   STA 2003H      ; remainder
        MOV A, D
        STA 2002H      ; quotient
        HLT
```

Assumes divisor is non-zero. A zero divisor would loop forever.

### e) Find the smallest element of an array

Length at 2000H, array from 2001H onward, result at 3000H.

```asm
        LXI H, 2000H
        MOV C, M       ; C = count
        INX H
        MOV A, M       ; assume first element is smallest
        DCR C
        JZ STORE       ; only one element
LOOP:   INX H
        CMP M          ; A - [HL], carry set if A < M
        JC SKIP        ; A is already smaller
        MOV A, M       ; otherwise M is smaller or equal
SKIP:   DCR C
        JNZ LOOP
STORE:  STA 3000H
        HLT
```

**For the largest element:** change `JC SKIP` to `JNC SKIP`.

---

## 3. Memory Hierarchy

### Definition

Memory hierarchy arranges storage in levels. Going down the levels, **capacity increases, cost per bit falls, and speed drops**. The aim is to give the CPU the speed of the fastest memory at roughly the cost of the cheapest.

```
            ^ faster, costlier, smaller
        [ CPU Registers ]
        [ Cache Memory (L1, L2, L3) ]
        [ Main Memory (RAM) ]
        [ Secondary Storage (SSD, Magnetic Disk) ]
        [ Tertiary / Backup (Magnetic Tape, Optical) ]
            v slower, cheaper, larger
```

| Level       | Speed             | Size     | Role                                                 |
| ----------- | ----------------- | -------- | ---------------------------------------------------- |
| Registers   | Fastest (1 clock) | Bytes    | Hold operands inside the CPU                         |
| Cache       | Very fast (SRAM)  | KB to MB | Holds recently/frequently used data and instructions |
| Main memory | Fast (DRAM)       | GB       | Holds running programs and data                      |
| Secondary   | Slow              | GB to TB | Permanent storage, backing store for virtual memory  |
| Tertiary    | Slowest           | TB+      | Archival and backup                                  |

### Why it works: locality of reference

- **Temporal locality:** recently used items are likely to be used again soon.
- **Spatial locality:** items near a recently used address are likely to be used soon.

Most accesses are served by the fast upper levels, so the average access time stays low.

---

## 4. Isolated I/O vs Memory-Mapped I/O

Both are ways of assigning addresses to I/O devices (I/O interface registers).

| Point            | Isolated (I/O-mapped) I/O                          | Memory-mapped I/O                                                |
| ---------------- | -------------------------------------------------- | ---------------------------------------------------------------- |
| Address space    | Separate address space for I/O                     | I/O shares the memory address space                              |
| Control signals  | Separate `IO/M` signal and `IN`/`OUT` instructions | Same `MEMR`/`MEMW` signals as memory                             |
| Instructions     | Special: `IN`, `OUT`                               | Ordinary memory instructions (LDA, STA, MOV, etc.)               |
| Address size     | 8-bit port addresses (256 ports in 8085)           | Full 16-bit addresses                                            |
| Memory available | Full 64 KB for memory                              | Reduced, since I/O uses part of it                               |
| Hardware         | Needs extra control lines                          | Simpler control logic                                            |
| Operations       | Mostly only accumulator transfers                  | All memory instructions work (arithmetic, logic directly on I/O) |

**Isolated I/O**

- Advantages: full memory space remains available; I/O instructions make the code easy to identify; address decoding for ports is simple.
- Disadvantages: only `IN`/`OUT` can be used, mostly via the accumulator; extra control signals are needed; fewer ports.

**Memory-mapped I/O**

- Advantages: all memory instructions work on I/O; no special instructions or extra control lines; more devices can be addressed.
- Disadvantages: uses up part of the memory address space; the full 16-bit address must be decoded, so decoding is more complex and slower; I/O code is harder to distinguish from memory code.

---

## 5. SAP-1 and SAP-2

SAP = Simple-As-Possible computer (Malvino). A teaching architecture.

### SAP-1 components and block diagram

```
          +------------------- W BUS (8-bit) -------------------+
          |      |        |       |       |        |       |    |
        [PC]   [MAR]    [RAM]    [IR]    [A]    [Adder/   [B]  [Output
        4-bit  4-bit   16 x 8    8-bit   8-bit   Sub]     8-bit  Reg]
                                    |                             |
                          [Controller-Sequencer]            [Binary Display]
                                    |
                          (control word: 12 bits)
                         Clock -> Ring Counter (T1..T6)
```

| Component                         | Function                                                                      |
| --------------------------------- | ----------------------------------------------------------------------------- |
| **Program Counter (PC)**          | 4-bit; holds the address of the next instruction; increments after each fetch |
| **MAR** (Memory Address Register) | 4-bit; holds the address to be read from RAM                                  |
| **RAM**                           | 16 words x 8 bits; stores program and data                                    |
| **Instruction Register (IR)**     | 8-bit; upper nibble = opcode (to controller), lower nibble = address (to bus) |
| **Controller-Sequencer**          | Generates control words and timing (T1-T6)                                    |
| **Accumulator (A)**               | 8-bit; holds intermediate results                                             |
| **Adder/Subtractor**              | Adds or subtracts B from A                                                    |
| **B register**                    | 8-bit; second operand for arithmetic                                          |
| **Output register**               | Holds the result for the display                                              |
| **Binary display**                | Shows the output register contents                                            |
| **W bus**                         | 8-bit common bus connecting everything                                        |

### SAP-1 instruction set

| Instruction | Opcode | Operation                     |
| ----------- | ------ | ----------------------------- |
| LDA addr    | 0000   | Load A from memory            |
| ADD addr    | 0001   | A = A + [addr]                |
| SUB addr    | 0010   | A = A - [addr]                |
| OUT         | 1110   | Send A to the output register |
| HLT         | 1111   | Stop                          |

Each instruction uses 6 T-states: T1-T3 (fetch: address, increment, memory) and T4-T6 (execute).

### SAP-1 vs SAP-2

| Feature            | SAP-1                        | SAP-2                                        |
| ------------------ | ---------------------------- | -------------------------------------------- |
| PC / MAR           | 4-bit                        | 16-bit                                       |
| Memory             | 16 bytes                     | 64 KB                                        |
| Registers          | A, B                         | A, B, C, plus TMP; B and C are bidirectional |
| Instruction length | 1 byte                       | 1 to 3 bytes                                 |
| Instruction count  | 5                            | About 40                                     |
| Flags              | None                         | Sign and Zero flags                          |
| Branching          | None                         | Jump (JMP, JZ, JNZ, JM), CALL/RET            |
| Logic operations   | None                         | AND, OR, XOR, complement, rotate, INR/DCR    |
| I/O                | One output register          | Input and output ports                       |
| Control            | Fixed 6 T-state ring counter | Variable machine cycles per instruction      |

**Bidirectional registers:** In SAP-2, registers B and C (and TMP) can both send data to and receive data from the bus, so they can serve as general data registers.

---

## 6. Flags in 8085

The flag register is 8 bits, but only **5 flags** are used. A flag is a 1-bit flip-flop that records the status of the last arithmetic or logic operation.

```
Bit:   D7  D6  D5  D4  D3  D2  D1  D0
Flag:  S   Z   X   AC  X   P   X   CY
```

(X = unused)

| Flag   | Name            | Set (1) when                                               |
| ------ | --------------- | ---------------------------------------------------------- |
| **S**  | Sign            | Result's MSB (D7) is 1, meaning negative in 2's complement |
| **Z**  | Zero            | Result is zero                                             |
| **AC** | Auxiliary Carry | Carry from bit 3 to bit 4; used for BCD (DAA)              |
| **P**  | Parity          | Result has an even number of 1s                            |
| **CY** | Carry           | Carry out of bit 7 in addition, or a borrow in subtraction |

Flags are tested by conditional jumps such as JZ, JNZ, JC, JNC, JP, JM, JPE, JPO.

---

## 7. RISC vs CISC

| Feature           | RISC                                   | CISC                                     |
| ----------------- | -------------------------------------- | ---------------------------------------- |
| Full form         | Reduced Instruction Set Computer       | Complex Instruction Set Computer         |
| Instruction set   | Small, simple                          | Large, complex                           |
| Instruction size  | Fixed length                           | Variable length                          |
| Execution         | Mostly one clock cycle per instruction | Multiple cycles per instruction          |
| Addressing modes  | Few                                    | Many                                     |
| Memory access     | Only LOAD/STORE touch memory           | Many instructions access memory directly |
| Registers         | Many (large register file)             | Fewer                                    |
| Control unit      | Hardwired                              | Usually microprogrammed                  |
| Pipelining        | Easy and highly efficient              | Difficult                                |
| Code size         | Larger programs                        | Smaller programs                         |
| Complexity burden | On the compiler                        | On the hardware                          |
| Examples          | ARM, MIPS, SPARC                       | Intel x86, VAX                           |

---

## 8. Control Unit and Microprogramming

### What is a control unit?

The control unit is the part of the CPU that generates timing and control signals to fetch, decode, and execute instructions. It tells the ALU, registers, memory, and I/O what to do at each clock step.

### Hardwired control unit: block diagram

```
 Instruction Register (opcode)
          |
   [3 x 8 Decoder] ---> D0..D7  ---+
                                   |
   I (indirect) bit ---------------+
                                   v
 Clock -> [Sequence Counter SC] -> [4 x 16 Decoder] -> T0..T15 --> [ CONTROL LOGIC GATES ] --> Control signals
                 ^                                                      ^         |        (load, increment,
                 |                                                      |         |         clear, read/write,
                 +----------------- clear SC <--------------------------+         |         ALU operations)
                                                       Status inputs (flags, E, R, IEN, FGI, FGO, AC, DR bits)
```

### Function of each unit

- **Instruction Register (IR):** holds the current instruction; its opcode bits feed the decoder.
- **Instruction decoder (3 x 8):** decodes the opcode into one of D0-D7 lines.
- **Sequence counter (SC) and timing decoder (4 x 16):** the SC counts clock pulses and the decoder converts the count into timing signals T0-T15, giving each step a separate time slot.
- **Control logic gates:** combinational circuit (AND/OR gates) that takes decoded opcode, timing signals, I bit, and status flags as inputs and generates all control signals.
- **Status/flag inputs:** let the signals depend on conditions (e.g., zero flag, interrupt flag).
- **Outputs:** signals that load, increment, or clear registers, select ALU operations, and read or write memory; one output clears SC to restart the cycle.

### Microprogrammed control unit

Control signals are stored as **microinstructions** in a **control memory (control ROM)** instead of being generated by gates. Components: control address register (CAR), control memory, control data register (pipeline register), and next-address generator (sequencer).

### Hardwired vs microprogrammed

| Feature        | Hardwired                           | Microprogrammed                             |
| -------------- | ----------------------------------- | ------------------------------------------- |
| Implementation | Gates, decoders, flip-flops         | Control memory (ROM) with microprogram      |
| Speed          | Faster                              | Slower (control memory access)              |
| Flexibility    | Hard to modify; redesign needed     | Easy to modify by changing the microprogram |
| Design         | Complex, error-prone                | Systematic, easier to design                |
| Cost           | Costly for complex instruction sets | Cheaper for complex instruction sets        |
| Used in        | RISC                                | CISC                                        |

### Definitions

- **Micro-operation:** a single elementary operation on data in registers (e.g., `AR <- PC`).
- **Microinstruction:** a control word in control memory specifying one or more micro-operations.
- **Microprogram:** a sequence of microinstructions that implements one machine instruction.
- **Main memory** stores machine-level program and data; **control memory** is a separate ROM that stores the microprograms.

### Symbolic microprogram for FETCH (Mano)

```
ORG 64
FETCH:  PCTAR     U   JMP   NEXT        ; AR <- PC
        READ, INCPC U JMP   NEXT        ; DR <- M[AR], PC <- PC + 1
        DRTAR     U   MAP               ; AR <- DR(0-10), CAR(2-5) <- DR(11-14), CAR(0,1,6) <- 0
```

| Microinstruction | Micro-operation                                                                                         |
| ---------------- | ------------------------------------------------------------------------------------------------------- |
| PCTAR            | AR <- PC (address placed in AR)                                                                         |
| READ, INCPC      | DR <- M[AR], PC <- PC + 1 (read instruction, increment PC)                                              |
| DRTAR + MAP      | AR <- DR(0-10) (address part), then map the opcode to the first microinstruction address of the routine |

`U` = unconditional, `JMP NEXT` = go to the next address, `MAP` = jump to the address derived from the opcode.

### Binary form of the FETCH microprogram

Microinstruction format (20 bits): `F1(3) F2(3) F3(3) CD(2) BR(2) AD(7)`

| Address      | F1  | F2  | F3  | CD  | BR  | AD      |
| ------------ | --- | --- | --- | --- | --- | ------- |
| 1000000 (64) | 110 | 000 | 000 | 00  | 00  | 1000001 |
| 1000001 (65) | 000 | 100 | 101 | 00  | 00  | 1000010 |
| 1000010 (66) | 101 | 000 | 000 | 00  | 11  | 0000000 |

### Symbolic microprogram for ADD

```
ADD:    NOP         I   CALL  INDRCT    ; if indirect, call the indirect routine
        READ        U   JMP   NEXT      ; DR <- M[AR]
        ADD         U   JMP   FETCH     ; AC <- AC + DR, then go to FETCH
```

---

## 9. Arithmetic Micro-operations

Basic arithmetic micro-operations: **addition, subtraction, increment, decrement, transfer/complement.**

| Micro-operation | Symbolic             | Meaning                       |
| --------------- | -------------------- | ----------------------------- |
| Add             | `R3 <- R1 + R2`      | Sum of R1 and R2 placed in R3 |
| Subtract        | `R3 <- R1 + R2' + 1` | R1 plus 2's complement of R2  |
| Increment       | `R1 <- R1 + 1`       | Add 1 to R1                   |
| Decrement       | `R1 <- R1 - 1`       | Subtract 1 from R1            |
| Complement      | `R2 <- R2'`          | 1's complement                |
| Negate          | `R2 <- R2' + 1`      | 2's complement                |
| Transfer        | `R2 <- R1`           | Copy R1 to R2                 |

### Hardware implementation

- **Addition:** a **binary adder**, built from full adders connected in a chain (ripple carry).
- **Subtraction:** **adder-subtractor**: XOR gates on the B inputs controlled by a mode bit M. When M = 0 it adds; when M = 1 it complements B and sets carry-in = 1, giving A + B' + 1.
- **Increment:** a **half-adder chain** that adds 1 to A (the input carry = 1).
- **Decrement:** add all 1s (the 2's complement of 1), i.e. A + 1111.

### 4-bit decrementer using four full adders (A <- A - 1)

```
A3  A2  A1  A0
 |   |   |   |
[FA][FA][FA][FA]      Second input of every FA tied to 1 (B = 1111)
 ^                    Carry-in of FA0 = 0
 | carry chain        Carry-out of FA3 is ignored
 S3  S2  S1  S0  = A - 1
```

**Explanation:** A - 1 = A + (2's complement of 1) = A + 1111 (in 4 bits). So each full adder gets one bit of A and a constant 1, with initial carry 0. The sum outputs give A - 1, and the final carry is discarded.

---

## 10. 8085 Architecture

### What is a microprocessor?

A microprocessor is a programmable, multipurpose integrated circuit (CPU on a single chip) that fetches instructions from memory, decodes them, and performs arithmetic, logic, and control operations on data.

### Three categories of microprocessor functions

1. **Microprocessor-initiated operations:** memory read/write, I/O read/write.
2. **Internal operations:** data storage in registers, arithmetic and logic (ALU), instruction decoding, and tests for condition.
3. **Peripheral (externally initiated) operations:** reset, interrupt, ready, hold (DMA).

### 8085 key facts

8-bit microprocessor, 40-pin DIP, +5 V supply, single-phase clock, 16-bit address bus (64 KB memory), 8-bit data bus, multiplexed lower address/data bus (AD0-AD7), 5 interrupts, serial I/O (SID, SOD).

### Block diagram

```
  +--------------------------------------------------------------------+
  |  Interrupt Control        Serial I/O Control                       |
  |  (TRAP, RST7.5/6.5/5.5,   (SID, SOD)                               |
  |   INTR, INTA)                                                      |
  |                                                                    |
  |  [Accumulator]  [Temp Reg]   [Flag Register]    [Instruction Reg]  |
  |        \           |          /                        |           |
  |         \-------[   ALU   ]--/                [Instruction Decoder |
  |                                                  & Machine Cycle   |
  |  [B] [C]  [D] [E]  [H] [L]   [W] [Z]             Encoding]         |
  |                                                       |            |
  |  [Stack Pointer 16-bit]  [Program Counter 16-bit]  [Timing and     |
  |  [Incrementer/Decrementer Address Latch]            Control Unit]  |
  |                                                                    |
  |  [Address Buffer] [Address/Data Buffer]            Control Signals |
  +----------A15-A8--------AD7-AD0---------------------RD WR ALE IO/M-+
```

### Functional units

| Unit                                   | Function                                                                                     |
| -------------------------------------- | -------------------------------------------------------------------------------------------- |
| **ALU**                                | Performs arithmetic (add, subtract, inc, dec) and logic (AND, OR, XOR, compare, rotate)      |
| **Accumulator (A)**                    | 8-bit register; holds one operand and receives the result                                    |
| **Temporary register**                 | Holds the second ALU operand; not accessible to the programmer                               |
| **Flag register**                      | 5 flags: S, Z, AC, P, CY                                                                     |
| **General registers B, C, D, E, H, L** | 8-bit each; usable as pairs BC, DE, HL; HL also serves as the memory pointer (M)             |
| **W, Z registers**                     | Temporary registers used internally by the processor (not programmer-accessible)             |
| **Program Counter (PC)**               | 16-bit; holds the address of the next instruction                                            |
| **Stack Pointer (SP)**                 | 16-bit; points to the top of the stack in memory                                             |
| **Instruction register and decoder**   | Holds the opcode and decodes it                                                              |
| **Timing and control unit**            | Generates timing and control signals (RD, WR, ALE, IO/M, S0, S1) and synchronizes everything |
| **Interrupt control**                  | Handles TRAP, RST 7.5, RST 6.5, RST 5.5, INTR                                                |
| **Serial I/O control**                 | Serial data in (SID) and out (SOD) via RIM/SIM                                               |
| **Address buffer (A8-A15)**            | Unidirectional, high-order address lines                                                     |
| **Address/data buffer (AD0-AD7)**      | Bidirectional, multiplexed; ALE separates address from data                                  |

### Bus system

- **Address bus:** 16 lines, unidirectional, addresses 2^16 = 64 KB.
- **Data bus:** 8 lines, bidirectional.
- **Control bus:** RD, WR, ALE, IO/M, READY, HOLD, HLDA, RESET, etc.

---

## 11. Addressing Modes and 8085 Instructions

An addressing mode is the way an instruction specifies where its operand is. 8085 has **5 modes**:

| Mode                   | Operand location                                        | Example                                        |
| ---------------------- | ------------------------------------------------------- | ---------------------------------------------- |
| **Immediate**          | The data is in the instruction itself                   | `MVI B, 05H`, `LXI H, 2050H`, `ADI 0AH`        |
| **Register**           | In a CPU register                                       | `MOV A, B`, `ADD C`                            |
| **Direct**             | The instruction holds the memory address of the operand | `LDA 2050H`, `STA 4000H`, `IN 01H`             |
| **Register indirect**  | A register pair holds the memory address                | `MOV A, M` (address in HL), `LDAX B`, `STAX D` |
| **Implied (implicit)** | The operand is implied by the opcode                    | `CMA`, `RAL`, `STC`, `HLT`                     |

### STA 4000H: function and type

- **Function:** stores (copies) the contents of the accumulator into memory location 4000H.
- **Type:** **Direct addressing.** The 16-bit memory address (4000H) is written explicitly in the instruction.
- **Encoding:** 3 bytes: `32H` (opcode), `00H` (low address), `40H` (high address); low byte first.
- **Timing:** 4 machine cycles, 13 T-states. No flags are affected.

### Instruction groups

- **Data transfer:** MOV, MVI, LDA, STA, LXI, LDAX, STAX, XCHG, IN, OUT
- **Arithmetic:** ADD, ADI, SUB, SUI, INR, DCR, INX, DCX, DAD
- **Logic:** ANA, ORA, XRA, CMP, CMA, RLC, RRC, RAL, RAR
- **Branching:** JMP, JZ, JNZ, JC, JNC, CALL, RET
- **Control:** HLT, NOP, EI, DI

### Five arithmetic instructions with examples

| Instruction | Operation                            | Example                        |
| ----------- | ------------------------------------ | ------------------------------ |
| `ADD B`     | A = A + B                            | A = 20H, B = 10H, then A = 30H |
| `ADI 05H`   | A = A + 05H (immediate)              | A = 20H, then A = 25H          |
| `SUB C`     | A = A - C                            | A = 30H, C = 10H, then A = 20H |
| `INR B`     | B = B + 1 (flags except CY affected) | B = 0FH, then B = 10H          |
| `DCR C`     | C = C - 1 (flags except CY affected) | C = 10H, then C = 0FH          |

Other arithmetic instructions: `DAD B` (HL = HL + BC), `INX H` (HL = HL + 1; no flags affected).

---

## 12. Booth Multiplication

### Procedure

Used for multiplying signed numbers in 2's complement form.

Registers: **M** = multiplicand, **Q** = multiplier, **AC** = 0, **Q(-1)** = 0, counter = number of bits.

1. Look at **Q0 and Q(-1)**:
   - `10`: AC = AC - M
   - `01`: AC = AC + M
   - `00` or `11`: no operation
2. **Arithmetic shift right** the combined AC, Q, Q(-1) (sign bit of AC is preserved).
3. Decrement the counter. If not zero, repeat from step 1.
4. The product is in AC:Q.

### Example 1: 9 x 7 (5-bit)

M = 9 = 01001, -M = 10111, Q = 7 = 00111

| Step | Q0 Q(-1) | Operation   | AC    | Q     | Q(-1) |
| ---- | -------- | ----------- | ----- | ----- | ----- |
| Init |          |             | 00000 | 00111 | 0     |
| 1    | 10       | AC = AC - M | 10111 | 00111 | 0     |
|      |          | ASR         | 11011 | 10011 | 1     |
| 2    | 11       | ASR         | 11101 | 11001 | 1     |
| 3    | 11       | ASR         | 11110 | 11100 | 1     |
| 4    | 01       | AC = AC + M | 00111 | 11100 | 1     |
|      |          | ASR         | 00011 | 11110 | 0     |
| 5    | 00       | ASR         | 00001 | 11111 | 0     |

Result AC:Q = 0000111111 = **63** ✓

### Example 2: (-9) x (-13) (5-bit)

M = -9 = 10111, -M = 01001, Q = -13 = 10011

| Step | Q0 Q(-1) | Operation   | AC    | Q     | Q(-1) |
| ---- | -------- | ----------- | ----- | ----- | ----- |
| Init |          |             | 00000 | 10011 | 0     |
| 1    | 10       | AC = AC - M | 01001 | 10011 | 0     |
|      |          | ASR         | 00100 | 11001 | 1     |
| 2    | 11       | ASR         | 00010 | 01100 | 1     |
| 3    | 01       | AC = AC + M | 11001 | 01100 | 1     |
|      |          | ASR         | 11100 | 10110 | 0     |
| 4    | 00       | ASR         | 11110 | 01011 | 0     |
| 5    | 10       | AC = AC - M | 00111 | 01011 | 0     |
|      |          | ASR         | 00011 | 10101 | 1     |

Result AC:Q = 0001110101 = **117** ✓

---

## 13. Restoring Division

### Algorithm

Registers: **A** = 0 (extra sign bit), **Q** = dividend, **M** = divisor. Repeat n times (n = bits in Q):

1. Shift left the combined A:Q by one bit.
2. A = A - M.
3. If A is negative (MSB = 1): set Q0 = 0 and **restore** A = A + M.
   If A is positive: set Q0 = 1.
4. Decrement the counter. Repeat until zero.

Final: Q = quotient, A = remainder.

### Example 1: Question from 2080 paper (AQ = 10100011, B = 1011)

> **Note:** The paper says 194 / 10, but the bits given (10100011 and 1011) are actually 163 / 11. Also, 194 / 10 = 19 does not fit in a 4-bit quotient. In the exam, work with the bits given and state this clearly.

163 / 11 → A = 01010 (5-bit, upper nibble 1010), Q = 0011, M = 01011, -M = 10101.

| Iteration | Operation       | A                | Q    |
| --------- | --------------- | ---------------- | ---- |
| Init      |                 | 01010            | 0011 |
| 1         | Shift left      | 10100            | 011_ |
|           | A = A - M       | 01001 (positive) |      |
|           | Q0 = 1          | 01001            | 0111 |
| 2         | Shift left      | 10010            | 111_ |
|           | A = A - M       | 00111 (positive) |      |
|           | Q0 = 1          | 00111            | 1111 |
| 3         | Shift left      | 01111            | 111_ |
|           | A = A - M       | 00100 (positive) |      |
|           | Q0 = 1          | 00100            | 1111 |
| 4         | Shift left      | 01001            | 111_ |
|           | A = A - M       | 11110 (negative) |      |
|           | Q0 = 0, restore | 01001            | 1110 |

**Quotient = 1110 = 14, Remainder = 01001 = 9.** Check: 14 x 11 + 9 = 163 ✓

### Example 2: 448 / 17 (2079 paper)

448 = 0111000000, 17 = 10001. Use a 6-bit A: A = 001110, Q = 00000, M = 010001, -M = 101111.

| Iteration | Operation                                         | A      | Q     |
| --------- | ------------------------------------------------- | ------ | ----- |
| Init      |                                                   | 001110 | 00000 |
| 1         | Shift, A - M = 001011 (positive), Q0 = 1          | 001011 | 00001 |
| 2         | Shift, A - M = 000101 (positive), Q0 = 1          | 000101 | 00011 |
| 3         | Shift, A - M = 111001 (negative), Q0 = 0, restore | 001010 | 00110 |
| 4         | Shift, A - M = 000011 (positive), Q0 = 1          | 000011 | 01101 |
| 5         | Shift, A - M = 110101 (negative), Q0 = 0, restore | 000110 | 11010 |

**Quotient = 11010 = 26, Remainder = 000110 = 6.** Check: 26 x 17 + 6 = 448 ✓

---

## 14. DMA

### Definition

Direct Memory Access (DMA) is a method of transferring data directly between an I/O device and main memory **without involving the CPU in each transfer**. It is used for fast, bulk transfers (disk, network).

### DMA controller: components

- **Address register:** holds the starting memory address; incremented after each transfer.
- **Word count register:** number of words to transfer; decremented after each transfer.
- **Control register:** mode and direction (read/write).
- **Data and address bus buffers**, **DMA select**, **RD/WR**, **bus request (BR/HOLD) and bus grant (BG/HLDA)**, **interrupt** lines.

### Basic DMA procedure

1. The CPU initializes the DMA controller: it loads the starting address, word count, and direction of transfer.
2. The I/O device sends a DMA request (DREQ) to the DMA controller.
3. The controller sends a **bus request (HOLD)** to the CPU.
4. The CPU finishes its current bus cycle, tri-states its buses, and sends a **bus grant (HLDA)**.
5. The DMA controller takes control of the buses and sends the memory address and read/write signals; data moves directly between the device and memory.
6. After each word, the address register is incremented and the word count decremented.
7. When the word count reaches zero, the controller releases the bus and sends an **interrupt** to the CPU signalling completion.

### Transfer modes

- **Burst (block) mode:** the controller keeps the bus until the whole block is transferred.
- **Cycle stealing:** the controller takes the bus for one word at a time, then releases it.
- **Transparent mode:** the controller uses the bus only when the CPU isn't using it.

### Role of the DMA controller

It takes over bus management from the CPU for the transfer: it generates addresses, controls read/write, counts words, arbitrates bus ownership, and notifies the CPU on completion. The CPU is free to do other work meanwhile.

---

## 15. Virtual Memory and Page Replacement

### Virtual memory

Virtual memory is a technique that lets programs use an address space (**virtual/logical address space**) larger than the physical main memory. The OS and hardware keep the active parts in main memory and the rest on disk, and move parts in and out as needed.

- The program uses **virtual addresses**; the hardware translates them to **physical addresses**.
- Memory is divided into fixed-size **pages** (virtual) and **page frames** (physical).
- Advantages: programs larger than RAM can run; more programs can run at once; each program has a simple, contiguous view of memory.

### Address mapping with pages

```
Virtual address = [ Page number | Line (offset) ]
                         |
                    [ Page Table ]  (indexed by page number)
                         |  gives: Frame number + Presence bit
                         v
Physical address = [ Frame number | Line (offset) ]
```

- Each page table entry has a **presence bit**: 1 = page is in memory, 0 = not in memory.
- If the presence bit is 0, a **page fault** occurs: the OS fetches the page from disk into a free frame, updates the page table, and restarts the instruction.

### Page replacement

When a page fault occurs and **no frame is free**, a page already in memory must be replaced.

| Algorithm   | Rule                                                                                                   |
| ----------- | ------------------------------------------------------------------------------------------------------ |
| **FIFO**    | Replace the page that has been in memory longest                                                       |
| **LRU**     | Replace the page not used for the longest time                                                         |
| **Optimal** | Replace the page that will not be used for the longest time in the future (ideal; used as a benchmark) |

**Example:** reference string 7, 0, 1, 2, 0, 3, 0, 4, 2, 3 with 3 frames.

- **FIFO:** 9 page faults (only the second reference to 0 is a hit).
- **LRU:** 8 page faults (hits on both references to 0 after the first).

FIFO is simple but can replace heavily used pages; LRU performs better but needs more hardware or bookkeeping.

---

## 16. Number Representation and Complements

### Signed number representation

For an 8-bit number, MSB = sign bit (0 = positive, 1 = negative).

| Form                 | How                                                  |
| -------------------- | ---------------------------------------------------- |
| **Signed magnitude** | Sign bit + magnitude                                 |
| **1's complement**   | For negative: invert all bits of the positive number |
| **2's complement**   | For negative: 1's complement + 1                     |

### Represent (88)10

88 = 01011000 in 8-bit binary. For a positive number, all three forms are identical:

- **Signed magnitude:** 01011000
- **1's complement:** 01011000
- **2's complement:** 01011000

For comparison, **-88**:

- Signed magnitude: 11011000
- 1's complement: 10100111
- 2's complement: 10101000

### Subtraction using 9's and 10's complement (2082 question)

> The paper writes (1197)2, which is a typo; 1197 is not a valid binary number. Treat it as (1197)10 and say so in the exam.

Compute **1197 - 1234**.

**9's complement method**

1. 9's complement of 1234 = 9999 - 1234 = 8765
2. 1197 + 8765 = 9962 (no end-around carry)
3. No carry means the result is negative: take the 9's complement of 9962 = 0037
4. **Answer = -37**

**10's complement method**

1. 10's complement of 1234 = 8765 + 1 = 8766
2. 1197 + 8766 = 9963 (no carry out)
3. No carry means negative: take the 10's complement of 9963 = 0037
4. **Answer = -37**

(If a carry were produced, the answer would be positive: in 9's complement add the carry back (end-around carry); in 10's complement discard the carry.)

---

## 17. Quick Hits

### Instruction format of the basic computer (Mano, 16-bit)

```
Memory-reference:     | I (1) | Opcode (3) | Address (12) |
Register-reference:   | 0 | 111 | register operation (12) |
I/O-reference:        | 1 | 111 | I/O operation (12) |
```

- I = 0: direct addressing; I = 1: indirect.
- **Numerical (2079):** memory of 256K words x 32 bits: 256K = 2^18, so address = **18 bits**. One possible split of the 32-bit word: Mode (1 bit) + Opcode (13 bits) + Address (18 bits) = 32. State your assumption for the opcode field.

### Instruction cycle timing (2079)

**Q:** Clock = 5 MHz. Time to execute `MVI A, 08H`?

- Clock period T = 1 / 5 MHz = 0.2 µs.
- `MVI r, data` = 2 machine cycles (opcode fetch 4 T-states + memory read 3 T-states) = **7 T-states**.
- Time = 7 x 0.2 µs = **1.4 µs**.

**Instruction cycle:** the complete time to fetch and execute one instruction; it consists of one or more machine cycles, each of which consists of several T-states (clock periods).

### Selective set (logic micro-operation)

Sets chosen bits of A to 1, using a mask B: `A <- A OR B`. Bits where B = 1 become 1; the others are unchanged. **Hardware:** one OR gate per bit with inputs A(i) and B(i).

### Multiplexed address/data bus (8085)

The lower 8 address lines and the 8 data lines share the same pins (AD0-AD7) to save pins. During T1 they carry the lower address byte, which is captured by an external latch on the **ALE** signal. During the remaining T-states, the same pins carry data.
