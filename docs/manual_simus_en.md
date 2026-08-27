# SimuS
## Sapiens Processor Simulator
### User Manual

---

## 1. Introduction

SimuS (Sapiens Simulator) is an educational tool developed to simulate the operation of the Sapiens processor. This simulator allows students to write, compile, and execute programs in assembly language, visualizing the behavior of the processor, registers, flags, and memory in real time.

SimuS offers advanced debugging features, including step-by-step execution, breakpoints, memory visualization, and simulated input/output ports.

---

## 2. User Interface

The user interface language can be set to Portuguese, English, or Spanish by clicking one of the flags located in the upper corner of the main window.

The SimuS interface is divided into three main panels, each with specific functions to facilitate program development and debugging.

### 2.1. Left Panel - Editor and Execution

This panel contains three tabs that allow you to edit code, view errors, and monitor execution:

#### 2.1.1. Editor Tab

An assembly code editing area with the following features:

- Text editor with syntax highlighting for assembly code.
- Dark background to reduce visual fatigue during programming.
- Monospaced font (Consolas) for better code alignment.
- Support for comments (lines starting with a semicolon `;`).

#### 2.1.2. Errors Tab

Displays error messages generated during compilation:

- Lists all errors found in the source code.
- Each error shows the line number and a description of the issue.
- Clicking an error positions the cursor on the corresponding line in the editor.
- A red badge on the tab title indicates the number of errors found.

#### 2.1.3. Execution Tab

Visualization of the compiled code with debugging resources:

- Displays the assembly code along with memory addresses in hexadecimal.
- The current line of execution (PC - Program Counter) is highlighted in yellow.
- Labels are displayed in orange for easy identification.
- Click on any line to add/remove a breakpoint (marked in red on the address).
- Automatic scrolling to follow the program execution.

### 2.2. Central Panel - CPU and Controls

This panel concentrates all execution controls and the visualization of the CPU state:

#### 2.2.1. Control Buttons

Five distinctly colored buttons to control execution:

- **Step (Orange):** Executes a single instruction and pauses. Ideal for detailed debugging.
- **Run (Green):** Executes the program continuously at normal speed (50ms per instruction). It stops automatically at breakpoints or when encountering an HLT instruction.
- **Turbo (Pink):** Executes the program at high speed (1000 instructions per cycle). Useful for long programs. It also respects breakpoints.
- **Stop (Red):** Interrupts execution in any mode (Run or Turbo).
- **Reset (Black):** Resets the processor to its initial state after an HLT. It restores the PC, registers, and I/O ports, but preserves the memory contents.

#### 2.2.2. Status Bar

Displays the current state of the simulator in gray text below the control buttons. Messages include: *"Ready"*, *"Running..."*, *"TURBO - Running..."*, *"HALT - Program Finished"*, among others.

#### 2.2.3. Registers

Three boxes displaying the values of the main registers in hexadecimal:

- **AC (Accumulator):** 8-bit register used for arithmetic and logical operations (format: XX).
- **PC (Program Counter):** 16-bit register that points to the address of the next instruction (format: XXXX).
- **SP (Stack Pointer):** 16-bit register that points to the top of the stack (format: XXXX, initialized to FFFF).

#### 2.2.4. Current Instruction

A box with a dark background displaying the mnemonic of the instruction currently pointed to by the PC. Example: `LDA #0xFF`. This yellow-gold highlighted view makes it easy to track execution.

#### 2.2.5. Flags (Indicators)

Three visual indicators showing the state of the processor flags:

- **N (Negative):** Lights up in blue when the result of the last operation is negative (bit 7 = 1).
- **Z (Zero):** Lights up in blue when the result of the last operation is zero.
- **C (Carry):** Lights up in blue when there is an overflow/carry in the last arithmetic operation.

#### 2.2.6. Input/Output Ports

Simulated peripheral interface with four components:

- **Banner - Text:** A wide text display that shows ASCII characters sent by the OUT 3 instruction. It supports multiple lines and bidirectional text. Example: *"Sapiens 2.0"*.
- **Input (IN) - Hex/Bin:** A text field where the user types hexadecimal (00-FF) or binary (8-bit) values to be read by the IN 0 instruction. Press ENTER after typing to confirm the value. A green LED lights up when data is available.
- **Output (OUT) - Hex/Bin:** A hexadecimal/binary display showing the last value sent by the OUT 0 instruction. Format: XX or XXXXXXXX.
- **Status LED:** A green indicator that lights up when data is entered and confirmed in the input, making it available for reading via IN 1 (status port).

### 2.3. Right Panel - Memory Visualization

Displays the contents of the RAM memory in hexadecimal format with navigation features:

#### 2.3.1. Navigation Bar

Controls at the top of the memory panel:

- **Button ‹ (Previous):** Rewinds 256 bytes (32 lines) in the view.
- **Address Field:** A central text box showing the starting address of the view in hexadecimal (format: XXXX). You can type an address and press ENTER to navigate directly to it.
- **Button › (Next):** Advances 256 bytes (32 lines) in the view.
- **Button < (Previous):** Moves back 256 bytes (32 lines) in the view.
- **PC Button:** Automatically navigates to the current Program Counter address, centering the view on the instruction being executed.
- **SP Button:** Automatically navigates to the current Stack Pointer address, centering the view on the program stack.

#### 2.3.2. Memory Grid

Visualization in a hexadecimal grid with the following characteristics:

- Displays 32 lines of 8 bytes each (256 total bytes per screen).
- The left column shows the base address of each line in hexadecimal.
- The top header indicates the offset (+0 to +7) for each column.
- Bytes with a value of 00 are displayed in light gray for easy identification.
- The byte pointed to by the PC is highlighted with a yellow background.
- The byte pointed to by the SP is highlighted with a lilac background.
- A monospaced font ensures perfect alignment of the values.

---

## 3. File Toolbar

Located at the top of the left panel, it offers buttons for file management and auxiliary windows:

- **📂 Open:** Opens an assembly file from the disk (.txt, .asm, .sap). The content is loaded into the editor, replacing the current code. The file name is displayed on the Editor tab.
- **💾 Save As...:** Saves the current code from the editor to a file on disk. It opens a browser dialog to choose the name and location. Default extension: .asm.
- **✔ Compile:** Compiles the assembly code in the editor. If there are errors, the Errors tab is automatically activated with the list of issues. If compilation is successful, the compiled code is loaded into memory, and the Execution tab is shown. The PC is positioned at the address defined by the ORG directive.
- **Terminal:** Shows or hides the text console pop-up window. The window can be moved by dragging its title bar.
- **Video:** Shows or hides the virtual graphic display pop-up window. This window can also be moved by dragging its title bar.

### 3.1. Pop-up Windows

The Terminal and Video windows are independent floating windows. To reposition them, click and drag the top bar of the window. The red circular button on the title bar closes/hides the window.

---

## 4. Typical Workflow

Follow these steps to develop and execute programs in SimuS:

1. **Edit the Code:** In the Editor tab, write your assembly program. Use comments (;) to document the code. Remember to include the ORG directive to define the starting address and END to mark the end of the program.

2. **Compile:** Click the ✔ Compile button. If there are errors, correct them as indicated in the Errors tab and compile again.

3. **Set Breakpoints (Optional):** In the Execution tab, click on the lines where you want to pause execution. A red circle will appear on the address.

4. **Run:** Choose an execution mode:
   - Step: For detailed, instruction-by-instruction debugging.
   - Run: For normal speed execution with visual updates.
   - Turbo: For long programs, running at maximum speed.

5. **Monitor Execution:** Observe the registers, flags, memory, and I/O ports updating in real time. The current line is highlighted in yellow in the Execution tab.

6. **Interact with I/O:** When the program executes IN 0, type a hexadecimal value into the Input (Hex) field and press ENTER. Values sent via OUT are displayed automatically.

7. **Finish:** The program stops automatically when it encounters an HLT. Use the Reset button to restart and run again.

8. **Save:** Use 💾 Save As... to save your work to a file.

---

## 5. Sapiens Instruction Set

The Sapiens processor implements the following categories of instructions:

### 5.1. Data Transfer Instructions

| Mnemonic | Name | Description |
|-----------|------|-------------|
| LDA | Load Accumulator | Loads AC with a value from memory or an immediate value |
| STA | Store Accumulator | Stores AC into memory |
| LDS | Load Stack Pointer | Loads SP with a 16-bit value |
| STS | Store Stack Pointer | Stores SP into memory (16 bits) |

### 5.2. Arithmetic Instructions

| Mnemonic | Name | Description |
|-----------|------|-------------|
| ADD | Addition | AC = AC + operand (updates flags) |
| ADC | Add with Carry | AC = AC + operand + C (updates flags) |
| SUB | Subtraction | AC = AC - operand (updates flags) |
| SBC | Subtract with Carry | AC = AC - operand - C (updates flags) |

### 5.3. Logical Instructions

| Mnemonic | Name | Description |
|-----------|------|-------------|
| AND | Logical AND | AC = AC & operand (updates flags) |
| OR | Logical OR | AC = AC \| operand (updates flags) |
| XOR | Exclusive OR | AC = AC ^ operand (updates flags) |
| NOT | Logical NOT | AC = ~AC (updates flags) |

### 5.4. Shift Instructions

| Mnemonic | Name | Description |
|-----------|------|-------------|
| SHL | Shift Left | Shifts AC 1 bit to the left (bit 0 = 0, C receives bit 7) |
| SHR | Shift Right | Shifts AC 1 bit to the right logically (bit 7 = 0, C receives bit 0) |
| SRA | Shift Right Arithmetic | Shifts AC 1 bit to the right arithmetically (maintains bit 7) |

### 5.5. Flow Control Instructions

| Mnemonic | Name | Description |
|-----------|------|-------------|
| JMP | Jump | Jumps unconditionally to an address |
| JZ | Jump if Zero | Jumps if flag Z = 1 |
| JNZ | Jump if Not Zero | Jumps if flag Z = 0 |
| JN | Jump if Negative | Jumps if flag N = 1 |
| JP | Jump if Positive | Jumps if flag N = 0 |
| JC | Jump if Carry | Jumps if flag C = 1 |
| JNC | Jump if No Carry | Jumps if flag C = 0 |

### 5.6. Subroutine Instructions

| Mnemonic | Name | Description |
|-----------|------|-------------|
| JSR | Jump to Subroutine | Saves PC to the stack and jumps to the subroutine |
| RET | Return | Returns from a subroutine (recovers PC from the stack) |

### 5.7. Stack Instructions

| Mnemonic | Name | Description |
|-----------|------|-------------|
| PUSH | Push to Stack | Pushes AC onto the stack (mem[SP] = AC, then SP--) |
| POP | Pop from Stack | Pops from the stack to AC (SP++, then AC = mem[SP]) |

### 5.8. Input/Output Instructions

| Mnemonic | Name | Description |
|-----------|------|-------------|
| IN | Input | Reads data from the specified port into AC |
| OUT | Output | Sends AC to the specified port |

#### Available I/O Ports:

| Instruction | Function |
|-------------|----------|
| IN 0 | Reads the hexadecimal value typed by the user |
| IN 1 | Reads input status (1 = data available, 0 = no data) |
| OUT 0 | Sends AC to the hexadecimal output display |
| OUT 2 | Clears the text banner |
| OUT 3 | Sends an ASCII character to the text banner (appends to the end) |

### 5.9. Special Instructions

| Mnemonic | Name | Description |
|-----------|------|-------------|
| NOP | No Operation | Does nothing (can be used for timing) |
| HLT | Halt | Stops the processor execution |
| TRAP | Trap | Generates a service call |

#### Available TRAP Operations:

- The TRAP number is passed in the accumulator. Additional parameters are passed in the memory address of the operand.
- The `TRAP` instruction returns status codes in the accumulator, but it does not update the flags. Before testing the return value with `JZ` or `JNZ`, use an instruction that updates flags without changing the value, such as `OR #0`:

```asm
LDA #20
TRAP VIDEO_CONFIG
OR #0
JNZ ERROR
```

| Instruction | Function |
|-------------|----------|
| #0 | Clears the console terminal |
| #1 | Reads a character from the terminal and saves it in the accumulator and the operand's memory address |
| #2 | Writes a character from the operand's memory address to the terminal |
| #3 | Reads a string from the terminal and saves it at the operand's memory address |
| #4 | Writes a string starting from the operand address (until a NULL is found) |
| #5 | Delay (Waits from 0 to 65535 ms) |
| #6 | Beep (Audio Synthesizer). Receives frequency and duration as parameters |
| #7 | Returns a pseudo-random number between 0 and 99 in the accumulator |
| #20 | Configures the virtual graphic display. The operand points to a `DW base` block, where `base` is the start of video memory. |
| #21 | Clears video memory with one color. The operand points to `DB color`. |
| #22 | Draws one pixel. The operand points to `DB x, y, color`. |
| #23 | Draws a line. The operand points to `DB x0, y0, x1, y1, color`. |
| #24 | Draws a rectangle. The operand points to `DB x, y, width, height, color, filled`. |
| #25 | Draws a circle. The operand points to `DB cx, cy, radius, color, filled`. |

#### Virtual Graphic Display

The virtual graphic display has a resolution of 128 × 64 pixels. Video memory occupies 8192 consecutive bytes, with 1 byte per pixel. `TRAP #20` defines which region of the 64 KB memory is used as the video buffer. The base address must be aligned to a multiple of 256, and the area `base + 8192` must not exceed the memory limit.

The pixel layout is linear:

```text
address = base + (y * 128) + x
```

Colors use the 8-bit `RRRGGGBB` format:

| Value | Approximate color |
|-------|-------------------|
| `224` / `0xE0` | Red |
| `28` / `0x1C` | Green |
| `3` / `0x03` | Blue |
| `252` / `0xFC` | Yellow |
| `255` / `0xFF` | White |

Main return values for `TRAP #20`:

| AC | Meaning |
|----|---------|
| 0 | Success |
| 1 | Base address is not aligned to 256 bytes |
| 2 | Video area exceeds the memory limit |
| 4 | Used by graphic TRAPs when video has not been configured yet |

---

## 6. Addressing Modes

Sapiens supports four addressing modes, identified by the 2 most significant bits of the opcode:

| Bits | Mode | Example | Operation | Description |
|------|------|---------|-----------|-------------|
| 00 | Direct | `LDA 50` | `AC = mem[50]` | The operand is the memory address of the data |
| 01 | Indirect | `LDA @50` | `AC = mem[mem[50]]` | The operand points to an address containing the final address of the data |
| 10 | 8-bit Immediate | `LDA #10` | `AC = 10` | The operand is the byte following the instruction |
| 11 | 16-bit Immediate| `LDS #1000` | `SP = 1000` | The operand consists of the two bytes following the instruction |

### Notes on Addressing:

- Instructions without an operand (NOP, RET, PUSH, POP, etc.) ignore the addressing mode.
- Indexed Mode is not fully implemented — use with caution.
- The `@` prefix indicates indirect addressing, `#` indicates immediate, and its absence indicates direct addressing.

---

## 7. Operand Formats

Sapiens supports several types of formats for instruction operands:

- Decimal: 10 - The number without decorators.
- Binary: 0b01010101 or 01010101B.
- Hexadecimal: 0x05 or 05H (must start with a digit).

---

## 8. Assembler Directives

The SimuS assembler recognizes the following directives:

| Directive | Description | Example | Effect |
|-----------|-------------|---------|--------|
| `ORG address` | Defines the starting address of the program | `ORG 0` | Program starts at address 0 |
| `END` | Marks the end of the source code | `END` | Last line of the file |
| `DB value[, value...]` | Defines one or more bytes (8 bits) | `DB 0xFF, 10, 1010B` | Stores the byte list in memory |
| `DW value[, value...]` | Defines one or more words (16 bits) | `DW 0x1234, 1000` | Stores words in little-endian format |
| `DS quantity` | Defines space (reserves bytes) | `DS 10` | Reserves 10 zeroed bytes |
| `LABEL EQU value` | Defines a constant | `TESTE EQU 10` | TESTE will be equal to 10 |

> **Note:** for constants, use `LABEL EQU value` without a colon. The form `LABEL: EQU value` first creates a label at the current address and may not define the constant as expected.
>
### Use of Labels:

Labels can be defined before any instruction or directive, ending with a colon:

```assembly
LOOP:
    LDA VALUE
    JNZ LOOP

```

* Labels must start with a letter and can contain letters, numbers, and underscores.
* They are automatically converted to uppercase by the assembler.
* They can be used as operands in jump and memory access instructions.
* You can use `LABEL+offset` to access bytes following a label. The currently accepted offset range is 1 to 8. For example, if `WORD: DW 0x1234`, then `WORD` points to the low byte (`0x34`) and `WORD+1` points to the high byte (`0x12`).

---

## 9. Code Examples

### 9.1. Simple Echo

A program that waits for user input and echoes the value back:

```assembly
; Echo Program
ORG 0
LOOP:
    IN 1          ; Read status
    OR #0         ; Verify value
    JZ LOOP       ; Wait for data
    IN 0          ; Read value
    OUT 0         ; Display value
    HLT
END

```

### 9.2. Counter from 0 to 9

Counts from 0 to 9 and stops:

```assembly
; Counter
ORG 0
    LDA #0        ; Start at 0
LOOP:
    LDA CONT      ; Load counter
    OUT 0         ; Show value
    ADD #1        ; Increment
    STA CONT      ; Save counter value
    SUB #10       ; Compare with 10
    JNZ LOOP      ; Continue if != 10
    HLT
END
CONT:  DB 0 
```

### 9.3. Subroutine with Stack

Demonstrates the use of JSR, RET, and PUSH/POP:

```assembly
; Passing a parameter on the stack
; Result returned in the accumulator

ORG 0
    LDA #42          ; Subroutine parameter
    PUSH             ; Pushes the parameter onto the stack
    JSR DOBRO        ; JSR pushes the return address onto the stack
    OUT 0            ; Shows the result: 84
    HLT

DOBRO:
    ; When entering the subroutine, the top of the stack contains
    ; the return address placed there by JSR.
    ; Below it is the parameter pushed by the main program.

    POP              ; Low byte of the return address
    STA RET
    POP              ; High byte of the return address
    STA RET+1
    POP              ; Retrieves the parameter
    STA PARAM

    ; Computes PARAM * 2
    LDA PARAM
    ADD PARAM
    STA RESULT

    ; Restores the return address.
    ; RET first pops the low byte and then the high byte.
    ; Since PUSH stores the value and decrements SP, we push the high byte first.

    LDA RET+1
    PUSH
    LDA RET
    PUSH
    LDA RESULT       ; Returns the result in the accumulator
    RET

RET:    DW 0         ; Return address saved by the subroutine
PARAM:  DB 0
RESULT: DB 0

END 0
```

---

### 9.4. Virtual Graphic Display

Configures video memory at `0x4000`, clears the screen, draws a filled rectangle, a line, and a circle:

```assembly
ORG 0

MAIN:
    LDA #20
    TRAP VIDEO_CONFIG
    OR #0
    JNZ ERROR

    LDA #21
    TRAP CLEAR

    LDA #24
    TRAP RECTANGLE

    LDA #23
    TRAP LINE

    LDA #25
    TRAP CIRCLE

    HLT

ERROR:
    HLT

VIDEO_CONFIG:
    DW VIDEO_BASE

CLEAR:
    DB 3              ; blue

RECTANGLE:
    DB 48, 16, 32, 32, 224, 1

LINE:
    DB 0, 63, 127, 0, 28

CIRCLE:
    DB 64, 32, 18, 252, 0

VIDEO_BASE EQU 16384 ; 0x4000

END MAIN
```

---

## 10. Troubleshooting Common Issues

### Error: "Invalid Instruction"

* Check if the mnemonic is written correctly. Remember that the assembler is case-insensitive.

### Error: "Undefined Label"

* Make sure that the label used in the instruction was defined somewhere in the code with a colon (:).

### Program does not execute after compiling

* Check if you clicked Compile before trying to run. The green status light should show "Loaded" in the message.

### Breakpoint does not work

* Breakpoints only work on lines with executable instructions. Empty lines, comments, and directives cannot have breakpoints.

### Memory does not update during execution

* In Turbo mode, the interface does not update at every instruction to maintain maximum speed. Use Run or Step mode to see changes in real time.

### IN does not read the typed value

* Remember to press ENTER after typing the hexadecimal value. The green LED must light up, indicating that the data is ready.

### Graphic display does not show the drawing

* Check that the program executed `TRAP #20` before the other graphic TRAPs.
* After `TRAP #20`, use `OR #0` or `SUB #0` before `JZ/JNZ` to correctly test the value returned in AC.
* The video memory base must be a multiple of 256. A recommended value is `0x4000` (`16384`).
* Use `VIDEO_BASE EQU 16384` without a colon to define the constant.
* Click the **Video** button if the window is not visible.

---

## 11. Tips and Best Practices

* **Use comments generously:** Document the purpose of each section of code using lines starting with a semicolon (;).
* **Organize with labels:** Use descriptive names for labels (LOOP, START, END, CALCULATE, etc.) to make the code more readable.
* **Test incrementally:** Compile and test small parts of the program before adding more features.
* **Use breakpoints strategically:** Place breakpoints at critical points (start of loops, subroutine calls, decisions) to facilitate debugging.
* **Monitor flags:** Observe N, Z, and C during execution to understand how operations affect the processor state.
* **Always end with HLT:** Ensure that every execution path ends with an HLT instruction to avoid unpredictable behavior.
* **Save your work frequently:** Use the 💾 Save As... button regularly so you don’t lose progress.
* **Check the Memory tab:** During debugging, use the PC button to quickly navigate to the current instruction in the memory view.

---

## 12. Conclusion

SimuS is a complete tool for learning computer architecture and assembly programming. Through its intuitive interface and advanced debugging features, students can experiment with fundamental concepts such as:

* The fetch-decode-execute cycle
* The operation of registers and flags
* Memory organization
* The stack and subroutine calls
* Data input and output
* Different addressing modes

This manual covers the essential aspects of the simulator. For additional questions or technical support, consult the Sapiens processor documentation or contact the developer.

**Happy studying and happy programming!**
