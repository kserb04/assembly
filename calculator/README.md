# Calculator written in assembly
In memory at address 0x600, there is a data array, where each data item is a structure consisting of three 32-bit numbers. The first two numbers represent operands, and
the third number represents a computational operation that needs to be performed on them. The operations are denoted by the following values:
    - 0 - subtraction
    - 1 - addition
    - 2 - multiplication
    - 3 - division

The number of data items in the block is not predefined, but it is known that the block ends with a data item where the number at the operator position is 0xFFFFFFFF.

## Task
Write an ARM processor program that processes a block of data in such a way that it performs a specified arithmetic operation on two data items from the structure located
at the end of the structure. After performing the operation, the program writes a 32-bit 2's complement result to memory starting at address 0x2000. The resulting block
should be terminated with a 0xFFFFFFFF data item. You may assume that the result of the operation will never match the number used to terminate the resultant block.

Also write a subroutine DIVIDE that divides two numbers integer by successive subtraction method. The subroutine receives the parameters and returns the result via the stack.
Use the DIVIDE subprogram in the main program of your solution for the operation of dividing two data in the structure.
In case of division by zero, the subroutine returns 0. You can perform the multiplication operation with the mnemonic commands available for the ARM processor.
Multiplication and division operations must preserve the sign of the data (eg by multiplying a positive and a negative number,
the result will be a negative number). For all operations, you can assume that they will give the correct result within 32 bits.
Also, you can assume that the value with which the arithmetic operation is marked will always be 0, 1, 2 or 3,
except in the case of locking the block (when it will be equal to 0xFFFFFFFF).

## Example input
| # | Address   | Description | Data      |
|---|-----------|-------------|-----------|
|   | 0000 0600 | 1st operand | FFFF FEFF |
| 1 | 0000 0604 | 2nd operand | 0000 0010 |
|   | 0000 0608 | operation   | 0000 0003 |
|---|-----------|-------------|-----------|
|   | 0000 060C | 1st operand | 0000 01F4 |
| 2 | 0000 0610 | 2nd operand | FFFF FD44 |
|   | 0000 0614 | operation   | 0000 0000 |
|---|-----------|-------------|-----------|
|   | 0000 0618 | 1st operand | 0000 0003 |
| 3 | 0000 061C | 2nd operand | FFFF FFEC |
|   | 0000 0620 | operation   | 0000 0001 |
|---|-----------|-------------|-----------|
|   | 0000 0624 | 1st operand | FFFF FFFE |
| 4 | 0000 0628 | 2nd operand | 0000 000A |
|   | 0000 062C | operation   | 0000 0002 |
|---|-----------|-------------|-----------|
|   | 0000 0630 | 1st operand | FFFF F000 |
| 5 | 0000 0634 | 2nd operand | FFFF FFC0 |
|   | 0000 0638 | operation   | 0000 0003 |
|---|-----------|-------------|-----------|
|   | 0000 063C | 1st operand | 0000 0001 |
| 6 | 0000 0640 | 2nd operand | 0000 0004 |
|   | 0000 0644 | operation   | FFFF FFFF |


## Example output
| Address   | Result     |
|-----------|------------|
| 0000 2000 | FFFF FFF0 |
| 0000 2004 | 0000 04B0 |
| 0000 2008 | FFFF FFEF |
| 0000 200C | FFFF FFEC |
| 0000 2010 | 0000 0040 |
| 0000 2014 | FFFF FFFF |
