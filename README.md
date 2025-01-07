# 16-bit-Computer
Designed my own CPU, and custom 4 wide Instruction-Set and Assembly language for it

Instruction is 4 wide, and since word size is 2 bytes each instruction is in total 8 bytes
However, most of the instructions are contained within the lower byte, and the upper byte is used only to immediate values

The following instructions are in hexadecimal unless specified. There are 25 OPCODES (not including variations for immediate values)

# 1st word - OPCODES:
- ADD  0000 - USED FOR COPY AS WELL
- SUB  0001
- MUL  0002
- SHL  0003
- SHR  0004
- ROL  0005
- ROR  0006
- AHR  0007
- AND  0008
- OR   0009
- NOT  000A
- XOR  000B

BRANCHING: If condition is met, program counter is overridden to whatever byte is in the 4th word (also known as the 'destination' word)

For the following conditional statements, the 2nd and 3rd words (operands) are compared respectively:
- EQ   000C
- NEQ  000D
- LESS 000E
- LEQ  000F
--- Use upper four bits of lower byte now ---
- GT   0010 
- GTEQ 0020
- JUMP 0030 
- PUSH 0040 
- POP  0050

- CALL 0060
- RET  0070

- NOP  0080

FILLER INSTRUCTIONS
Only included for better code readability for instructions that only use one out of the two operands or don't use operands at all
- TO/TOWARDS/THE/LINE   0000

- ex. JUMP TO LINE (LABEL) - In this example we simply just jump to the number specified in LABEL, we do not use the operands at all

IMMEDIATE: Allows to hard code the operand value instead of taking a value from  register/memory/stack. 

- IMMEDIATE LEFT/1st OPERAND -  0b(0000001x 00000000)
- IMMEDIATE RIGHT/2nd OPERAND - 0b(000000x1 00000000)

Note: if you want you can have both the 1st and 2nd operands to take an immediate value as an input at the same time by having it as 0b(11 xxxx xxxx)

# 2ND/3RD word - OPERANDS

If IMMEDIATE is on, then value is directly taken

ex. 00000011 00000000 | 00000000 00000111 | 00000000 00000100 | 00000000 00000001  
In this example, the Opcode word is add, with the immediate for the left and operands turned on. The left and right operands have a raw value of 7 and 4 respectively. The destination word is set to reg_1
result: 7+4 = 11 is stored into reg_1

If IMMEDIATE is OFF, then refer to the following:
- 00 reg_0
- 01 reg_1
...
- 07 reg_7
- 08 mem_reg
- 09 mem (memory value is pulled from whatever address mem_reg is currently at)
- 0A input for 2nd operand
- 0B counter (pull current program counter)

# 4th word - DESTINATION 
- 00 reg_0
- 01 reg_1
...
- 07 reg_7
- 08 mem_reg
- 09 mem (data from operands is stored in memory at whatever mem_reg is currently at)
- 0A output
- 0B counter (way to manually overwrite program counter)





