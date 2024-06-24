# Assembly practice
This repo contains practice problems in assembly.

## Calculator
[calculator](./calculator)

The program processes the data block and performs the arithmetic operation on two data
items located at the end of the structure. It then writes the result to memory starting
at address 0x2000.

- The program loads a word from the memory location pointed by R1 into R0.
- It checks whether the operator is equal to 0xFFFFFFFF and if so, it ends the loop and the program.
- If not, it checks the operator and performs the corresponding arithmetic operation.
- The program then stores the result to the memory location pointed by R2 and increments both the pointers.
- The loop continues till the operator is 0xFFFFFFFF.

## Coffee machine
[coffee-machine](./coffee-machine)

This project is an implementation of a simple coffee machine using ARM assembly language.
The coffee machine has the capability to make coffee with milk, and its functionality is controlled by an ARM processor, General Purpose Input/Output (GPIO) circuits, and a Real-Time Clock (RTC) circuit.

### Components
Components:
- ARM Processor
- GPIO1 Circuit at address 0xFFFF0F00
- GPIO2 Circuit at address 0xFFFF0B00
- RTC Circuit at address 0xFFFF0E00

### Circuit
The GPIO2 circuit has a button connected to port A bit 0, and three LEDs connected to port A bits 5, 6, and 7, which represent red, yellow, and green LEDs, respectively.
The GPIO1 circuit has an LCD display connected to port B.
