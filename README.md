# VSDsquadron-mini-internship

The vsdsquadron mini is a development board based on the RISC-V architecture, featuring a 32-bit RISC-V core. It is equipped with 16KB of flash memory and 2KB of SRAM which runs at a clock speed of 24 MHz. The board includes 15 GPIO pins and supports communication protocols such as I2C, SPI, and USART.

During this internship, we will delve into the RISC-V architecture and explore the capabilities of the vsdsquadron mini microprocessor. Additionally, we will work on a project utilizing the vsdsquadron mini.

<details>
  <summary><b>Task 1:</b> C code to RISC-V instruction set</summary>

  Write a c program to count the sum from 1 to n. To do so install leafpad by using the command  
  `leafpad sum1ton.c &`   
  Create a file sum1ton.c then write a c program and save it.  
  ![Screenshot (184)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/d776d243-febb-4807-a8a3-dee49d9ed1d1)

  Compile the c program and verify the results using the following commands  
  `gcc sum1ton.c`  
  `./a.out`  
  ![image](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/835864ee-a9bb-4c77-81f7-f045e8bf7de2)

  ### RISC V
  To get the RISC V instruction type from C program  
  `riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c`  
  To view the output we use the command  
  `riscv64-unknown-elf-objdump -d sum2n.o | less`
  ![Screenshot (186)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/ddf069c9-8df3-4407-adda-982df3f4d0c8)

  This opens the output in the less editor, facilitating easier navigation. To locate the main function, we search for the keyword "main" using ?main. By employing a hexadecimal calculator, we can count the number of instructions executed in the main block by subtracting the address numbers displayed on the left. In this case, the main block contains 15 lines of instructions.

  Now we can use `-Ofast` instead of `-O1` and notice the difference between them.  
  `riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c`  
  ![Screenshot (187)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/97d6c1f8-a395-4f59-9ab6-c0ebf6308b5e)
  We can notice that for `-Ofast` the instruction is reduced to 12 lines rather than 15 lines  

</details>

<details>
  <summary><b>Task 2:</b> Write a simple c program for the clock cycle divider and compile it RISC V GCC</summary>

  The c program for Clock cycle divider is as follows  
  ![Screenshot (193)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/d90c081f-359b-414b-acbc-a516516a0e3d)

  ### Output  
  ![Screenshot (192)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/7495cff9-3037-4ced-a153-1562a6c09871)

  To get the RISC V instruction type from C program  
  `riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o clockdiv.o clockdiv.c`  
  ![Screenshot (194)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/eed650f3-fbae-40d9-81b1-ab758ba55cf8)

  To view the output we use the command  
  `riscv64-unknown-elf-objdump -d clockdiv.o | less`  
  ![Screenshot (191)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/de09b78c-2511-4717-9dad-2e3e94ba49a5)

</details>

<details>
  <summary><b>Task 3:</b> To observe the output of the compiled c program and object file(using SPIKE Simulation)</summary>

  ### To verify the output of the c program and RISC v instructions  
  The command used to compile and execute c program is  
  `gcc sum1ton.c`  
  `./a.out`  
  ![Screenshot (200)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/fd3ca90f-0ca3-4ebc-90c6-98176e252199)

  The command used to compile and execute object file is  
  `riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o clockdiv.o clockdiv.c`  
  `spike pk clockdiv.o`  
  ![Screenshot (201)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/1dd190fb-0b65-45ed-a42c-170ce5169feb)

  ### Debugging
  ![Screenshot (198)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/ed88fca1-9827-4ec7-b599-417d8d170f73)
  The command for debugging is  
  `spike -d pk clockdiv.o`  
  ![Screenshot (199)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/a625a898-7cac-4040-af90-7b22c8859e0f)
  The command `until pc 0 100b0` specifies that the instruction gets executed up to 100b0 address  
  To know the status of the register we can use `reg 0 register_name` for example `reg 0 a0` shows us what is present in the a0 register

</details>

<details>
  <summary><b>Task 4 :</b>To identify the instruction type of all the given instructions with its exact 32 bits of instruction code in the desired instruction type format</summary>

## Introduction
This report provides a detailed analysis of various RISC-V instructions. Each instruction is classified into its respective type (R, I, S, B) and its exact 32-bit binary encoding is provided.
### Instruction Formats in RISC-V

The instruction format of a processor defines how machine language instructions are structured and organized for execution. These instructions consist of bits (0s and 1s), each carrying information about data locations and operations. RISC-V has six instruction formats:

1. **R-format**
2. **I-format**
3. **S-format**
4. **B-format**
5. **U-format**
6. **J-format**

Let's delve into each instruction format with examples.

#### 1. R-type Instruction
In RV32, each instruction is 32 bits long. The "R" in R-type stands for "register," indicating that these instructions operate on registers, not memory locations. R-type instructions perform various arithmetic and logical operations. The 32-bit instruction is divided into six fields:

- **Opcode (7 bits):** Identifies the type of instruction format.
- **rd (5 bits):** Destination Register, stores the result of the operation.
- **func3 (3 bits):** Specifies the type of arithmetic or logical operation.
- **rs1 (5 bits):** Source Register 1, holds data for the operation.
- **rs2 (5 bits):** Source Register 2, holds additional data for the operation.
- **func7 (7 bits):** Further specifies the operation.

#### 2. I-type Instruction
In RV32, each instruction is 32 bits long. The "I" in I-type stands for "immediate," meaning these instructions use registers and an immediate value. I-type instructions are used for immediate and load operations. The 32-bit instruction is divided into five fields:

- **Opcode (7 bits):** Identifies the type of instruction format.
- **rd (5 bits):** Destination Register, stores the result of the operation.
- **func3 (3 bits):** Specifies the type of arithmetic or logical operation.
- **rs1 (5 bits):** Source Register, holds data for the operation.
- **Immediate (12 bits):** Signed immediate value, replacing the rs2 and func7 fields from R-type.

#### 3. S-type Instruction
In RV32, each instruction is 32 bits long. The "S" in S-type stands for "store," indicating these instructions store register values into memory. S-type instructions are used for store operations. The 32-bit instruction is divided into six fields:

- **Opcode (7 bits):** Identifies the type of instruction format.
- **Immediate (12 bits):** Signed immediate value, split into imm[11:5] and imm[4:0].
- **rs1 (5 bits):** Source Register 1, holds the value to be stored.
- **rs2 (5 bits):** Source Register 2, used in address calculation.
- **func3 (3 bits):** Specifies the width and type of the store operation.

#### 4. B-type Instruction
In RV32, each instruction is 32 bits long. The "B" in B-type stands for "branch," indicating these instructions are used for conditional branching. The 32-bit instruction is divided into eight fields:

- **Opcode (7 bits):** Identifies the type of instruction format.
- **Immediate (12 bits):** Signed immediate value, split across imm[12], imm[10:5], imm[4:1], and imm[11].
- **rs1 (5 bits):** Source Register 1, involved in the condition check.
- **rs2 (5 bits):** Source Register 2, involved in the condition check.
- **func3 (3 bits):** Specifies the branch condition.

If the condition is true, the Program Counter (PC) is updated by adding the immediate value. If false, the PC moves to the next instruction (PC + 4 bytes). Instructions are word-aligned (address in multiples of 4 bytes).

#### 5. U-type Instruction
In RV32, each instruction is 32 bits long. The "U" in U-type stands for "upper immediate," meaning these instructions transfer immediate data to the destination register. The 32-bit instruction is divided into three fields:

- **Opcode (7 bits):** Identifies the type of instruction format.
- **rd (5 bits):** Destination Register.
- **Immediate (20 bits):** Upper immediate value, used in LUI and AUIPC instructions.

For example, the instruction `lui x15, 0x13579` writes the immediate value 0x13579 to the upper 20 bits of the rd register (x15), resulting in `x15 = 0x13579000`.

#### 6. J-type Instruction
In RV32, each instruction is 32 bits long. The "J" in J-type stands for "jump," indicating these instructions implement jump operations. The 32-bit instruction is divided into six fields:

- **Opcode (7 bits):** Identifies the type of instruction format.
- **rd (5 bits):** Destination Register.
- **Immediate (20 bits):** Signed immediate value, divided into four fields.

J-type instructions, such as JAL, are used to jump to a specified memory location, often for implementing loops.

## Instruction Formats
- **R-Type**: Used for register-register operations.
- **I-Type**: Used for immediate values and load instructions.
- **S-Type**: Used for store instructions.
- **B-Type**: Used for branch instructions.

## Detailed Instruction Analysis

### R-Type Instructions
| Instruction | Opcode | Funct3 | Funct7 | Binary Encoding |
|-------------|--------|--------|--------|-----------------|
| ADD r1, r2, r3 | 0110011 | 000 | 0000000 | 0000000 00011 00010 000 00001 0110011 |
| SUB r3, r1, r2 | 0110011 | 000 | 0100000 | 0100000 00010 00001 000 00011 0110011 |
| AND r2, r1, r3 | 0110011 | 111 | 0000000 | 0000000 00011 00001 111 00010 0110011 |
| OR r8, r2, r5 | 0110011 | 110 | 0000000 | 0000000 00101 00010 110 01000 0110011 |
| XOR r8, r1, r4 | 0110011 | 100 | 0000000 | 0000000 00100 00001 100 01000 0110011 |
| SLT r10, r2, r4 | 0110011 | 010 | 0000000 | 0000000 00100 00010 010 01010 0110011 |
| SRL r16, r11, r2 | 0110011 | 101 | 0000000 | 0000000 00010 01011 101 10000 0110011 |
| SLL r15, r11, r2 | 0110011 | 001 | 0000000 | 0000000 00010 01011 001 01111 0110011 |

### I-Type Instructions
| Instruction | Opcode | Funct3 | Immediate | Binary Encoding |
|-------------|--------|--------|-----------|-----------------|
| ADDI r12, r3, 5 | 0010011 | 000 | 000000000101 | 000000000101 00011 000 01100 0010011 |
| LW r13, r11, 2 | 0000011 | 010 | 000000000010 | 000000000010 01011 010 01101 0000011 |

### S-Type Instructions
| Instruction | Opcode | Funct3 | Immediate | Binary Encoding |
|-------------|--------|--------|-----------|-----------------|
| SW r3, r1, 4 | 0100011 | 010 | 000000000100 | 0000000 00011 00001 010 00010 0100011 |

### B-Type Instructions
| Instruction | Opcode | Funct3 | Immediate | Binary Encoding |
|-------------|--------|--------|-----------|-----------------|
| BNE r0, r1, 20 | 1100011 | 001 | 000000001010 | 0000000 00001 00000 001 00101 1100011 |
| BEQ r0, r0, 15 | 1100011 | 000 | 000000000111 | 0000000 00000 00000 000 00111 1100011 |

## Summary
This  provides a clear analysis of the given RISC-V instructions. Each instruction is categorized by type and detailed with its binary encoding.
</details>

<details>
  <summary><b>Task 5: </b>By making use of RISCV Core: Verilog Netlist and Testbench, perform an experiment of Functional Simulation and observe the waveforms  </summary>
  
  > **NOTE:** Please note that the design of the RISCV architecture and the creation of its testbench are not part of this Research Internship. Instead, we will utilize the existing Verilog code and testbench for the RISCV that have already been developed. You can find these resources in the GitHub repository named iiitb_rv32i.

## About IVERILOG and GTKWave

Icarus Verilog is an implementation of the Verilog hardware description language. GTKWave is a comprehensive wave viewer based on GTK+ v1.2 for Unix and Win32. It can read AET files generated by the Verilog Structural Compiler, as well as standard Verilog VCD/EVCD files, and allows for their viewing.

## Commands to install iverilog and GTKWave
```
sudo apt update  
sudo apt install iverilog gtkwave
```  

<img width="905" alt="image" src="https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/619cbe0a-6947-4c7e-ad7f-ece429183456">

### Steps to Perform Functional Simulation of RISC-V

1.Create a new directory with your name using the following command:  
`mkdir <your_name>`

 2.Next, create two files with these commands:  
 `touch aksh27_rv32i.v`  
 `touch aksh27_rv32i_tb.v`  

 3.Copy the code from the reference GitHub repository and paste it into your Verilog and testbench files.

 4.To run and simulate the Verilog code, use this command:  
`iverilog -o aksh27_rv32i aksh27_rv32i.v aksh27_rv32i_tb.v`  
 `./aksh27_rv32i`  
 
 5.To view the simulation waveform in GTKWave, use the following command:  
 `gtkwave aksh27_rv32i.vcd`  

 ## Analysing the Output Waveform of various instructions  

 `1:ADD`  
 ![Screenshot (219)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/b41ea12c-8c4a-4655-b151-4b3179f18eeb)

 `2.SUB`  
 ![Screenshot (220)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/91ac8b02-55e4-4705-a102-ec1e1764be67)

`3.AND`  
![Screenshot (221)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/876725cd-2386-4cb9-bf9c-c9607433e924)

`4.OR`
![Screenshot (222)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/488f8fb6-44ab-4203-80ac-b594e092b2f6)

`5.XOR`
![Screenshot (223)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/513c6330-7dfc-474b-8923-e8bfac011618)

 `6.SLT`  
 ![Screenshot (224)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/b2910438-c836-4454-bc24-f9965ab82fbb)

</details>
  
<details>
  <summary><b>Task 6: </b>Overview of the project using VSDSquadron mini</summary>
  
## Mini Weather Station

### Overview

The Mini Weather Station is a simple and cost-effective project that integrates sensors to measure temperature, humidity, and atmospheric pressure. The data collected from the sensors is displayed on a 16x2 LCD screen. This project is ideal for beginners in electronics and programming, providing hands-on experience with sensor interfacing and data visualization.

### Components Required

- **CH32V003F4U6 Board**
  - The microcontroller board that will serve as the brain of the weather station.

- **DHT11 Sensor**
  - Used for measuring temperature and humidity.

- **BMP180 Sensor**
  - Used for measuring atmospheric pressure.

- **16x2 LCD Screen**
  - Display module for showing the collected data. Can be either I2C or parallel interface.

- **Breadboard**
  - For assembling the circuit without soldering.

- **Jumper Wires**
  - For making electrical connections between components.

- **10kΩ Potentiometer**
  - Used for adjusting the contrast of the LCD if using a parallel interface.

- **Power Supply**
  - To power the entire circuit, such as a USB cable or battery pack.

### Pinout Diagram

![WhatsApp Image 2024-07-09 at 2 43 17 PM](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/6300935e-3079-4afc-b4b1-23ea6695035a)


### Circuit Connections

#### DHT11 Sensor

| Pin  | Connection                     |
|------|--------------------------------|
| VCC  | 3.3V or 5V                     |
| GND  | GND                            |
| DATA | Connect to any available GPIO pin (PC0) |

#### BMP180 Sensor (I2C)

| Pin  | Connection                     |
|------|--------------------------------|
| VIN  | 3.3V                           |
| GND  | GND                            |
| SCL  | Connect to I2C clock pin (PA1) |
| SDA  | Connect to I2C data pin (PA2) |

#### 16x2 LCD Screen (I2C Interface)

| Pin  | Connection                     |
|------|--------------------------------|
| VCC  | 3.3V                           |
| GND  | GND                            |
| SCL  | Connect to I2C clock pin (e.g., PA1) |
| SDA  | Connect to I2C data pin (e.g., PA2) |

#### 16x2 LCD Screen (Parallel Interface)

| Pin  | Connection                      |
|------|---------------------------------|
| VSS  | GND                             |
| VDD  | 5V                              |
| V0   | Middle pin of 10kΩ potentiometer (other two ends connected to VCC and GND) |
| RS   | Any GPIO pin (PD1)        |
| RW   | GND                             |
| E    | Any GPIO pin (PD2)        |
| D4-D7| Any GPIO pins (PD3-PD6)   |
| A, K | (For backlight) A to 5V, K to GND |



## Code

(To be added)


</details>
  
