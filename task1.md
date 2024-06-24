# VSDsquadron-mini-internship
The vsdsquadron mini is a development board based on the RISC-V architecture, featuring a 32-bit RISC-V core. It is equipped with 16KB of flash memory and 2KB of SRAM which runs at a clock speed of 24 MHz. The board includes 15 GPIO pins and supports communication protocols such as I2C, SPI, and USART.

During this internship, we will delve into the RISC-V architecture and explore the capabilities of the vsdsquadron mini microprocessor. Additionally, we will work on a project utilizing the vsdsquadron mini.


### C code to RISC-V instruction set
Write a c program to count the sum from 1 to n. To do so install leafpad by using the command.
`leafpad sum1ton.c &` 
Create a file sum1ton.c .Write a c program and save it.
![image](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/92ba6c1a-5da1-4bf4-9fd4-5cbf26e16b63)

Compile the c program and verify the results using the following commands
`gcc sum1ton.c`.
`./a.out`.
![image](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/835864ee-a9bb-4c77-81f7-f045e8bf7de2)


### RISC V
To get the RISC V instruction type from C program.
`riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c`
To view the output we use the command.
`riscv64-unknown-elf-objdump -d sum2n.o | less`
![Screenshot (186)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/ddf069c9-8df3-4407-adda-982df3f4d0c8)

This opens the output in the less editor, facilitating easier navigation. To locate the main function, we search for the keyword "main" using ?main. By employing a hexadecimal calculator, we can count the number of instructions executed in the main block by subtracting the address numbers displayed on the left. In this case, the main block contains 15 lines of instructions.

Now we can use `-Ofast` instead of `-O1` and notice the difference between them.
`riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c`
![Screenshot (187)](https://github.com/akshaynet27/VSDSquadron-Mini-research-internship/assets/173434697/97d6c1f8-a395-4f59-9ab6-c0ebf6308b5e)
We can notice that for `-Ofast` the instruction is reduced to 12 lines rather than 15 lines



