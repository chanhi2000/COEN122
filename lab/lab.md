# PROJECT:
Design a Structural Model of a Pipelined CPU

## OBJECTIVE:
The project is to design a structural model of a pipelined CPU with 13 instructions using Verilog HDL.

## DESCRIPTION:
In this project, you are asked to design a 32-bit pipelined CPU for the given SCU Instruction Set Architecture (SCU ISA). The SCU ISA is described below.
- __Register file size__: 64 registers, each register 32 bits
- __PC__: 32 bits
- __Instruction format__: Each instruction is 32-bit wide, and consists of five fields (`opcode`, `rd`, `rs`, `rt`, and `unused`) the format is as follows

The 13 instructions are defined in the following table.

| Instruction | Symbol | `opcode` | `rd` | `rs` | `rt` | `function` |
| :---------- | :----- | :------: | :--: | :--: | :--: | :--------- |
| No operation | `NOP` | 0000 | `x` | `x` | `x` | No operation |
| Load PC | `LDPC rd` | 1111 | `rd` | `x` | `x` | $rd <- M[PC] |
| Load | `LD rd, rs` | 1110 | `rd` | `rs` | `x` | $rd <- M[$rs] |
| Store | `ST rd, rs` | 0011 | `x` | `rs` | `rt` | M[$rs] <- $rt |
| Add | `ADD rd, rs, rt` | 0100 | `rd` | `rs` | `rt` | $rd <- $rs + $rt |
| Increment | `INC rd, rs` | 0101 | `rd` | `rs` | `x` | $rd <- $rs + 1 |
| Negate | `NEG rd, rs` | 0110 | `rd` | `rs` | `x` | $rd <- -$rs |
| Subtract | `SUB rd, rs, rt` | 0111 | `rd` | `rs` | `rt` | $rd <- $rs - $rt |
| Jump | `J rs` | 1000 | `x` | `rs` | `x` | PC <- $rs |
| Branch if zero | `BRZ rs` | 1001 | `x` | `rs` | `x` | PC <- $rs, if Z=1 |
| Jump memory | `JM rs` | 1010 | `x` | `rs` | `x` | PC <- M[$rs] |
| Branch if negative | `BRN rs` | 1011 | `x` | `rs` | `x` | PC <- $rs, if N=1 |
| Sum | `SUM rd, rs, rt` | 0001 | `rd` | `rs` | `rt` | $rd=$$\sum_{\$rt-1}^{i=0}$$M[$rs+i]

Also, use the instructions in the SCU ISA to write two versions of assembly program of the computation of finding the sum of $$n$$ numbers below. 
$$
A=\sum_{i=1}^{n}{a_i}\tag{1}
$$
The first version does not use the SUM instruction and the second one uses the SUM instruction. 

You can create your new instructions to make the above coding easier. This computation will be used to test your CPU. You may not need five stages in your pipeline.

When you analyze the cycle time, you can use the following delay data: delay of memory (I and D memory): $$2\:\text{ns}$$., delay of register file: $$t1.5\:\text{ns}$$., delay of ALU (adders): $$2\:\text{ns}$$. Ignore the delays of all other components.

Use the ALU attached in the last page.

The last instruction SUM is optional. However, four extra points will be added to both coen 122 and 122L if the SUM instruction is implemented correctly in your CPU.

## Submission:  
1. The two versions of code for (1)  to TA on the Friday of the third week (5%)
2. __Your datapath and control (30%)__ on the Monday of week 8 to Dr. Shang
3. __Report (25%)__  Please submit a written report to the TA On the last Friday, including the following
	- abstract (short description or outline of the project), 
	- detailed description of the CPU design including the datapath and the truth table of your control.
	- test benchmarks/waveforms verifying the functions, 
	- assembly code for calculating the sum in (1). 
	- estimate the time need to execute your code for (1) based on your CPU design, and verify your estimate with simulation/waveform. 
4. __Demo (40%)__: You will demo your working programs to our TA. During the demo, the TA will provide you n random numbers and you will show the TA the result after running your program on your pipeline.  You will also be asked to perform random but related tasks (for instance, change the address of data and demo the modified program), and be prepared to answer related project questions. The purpose of these questions is to make sure that you understand the project thoroughly. 


#### FIGURE 01. ALU Block Diagram

#### FIGURE 02. ALU Truth Table
| Operation | out | ADD | INC | NEG | SUB |
| add | B+A | 1 | 0 | 0 | 0 |
| increment | B+1 | 0 | 1 | 0 | 0 |
| 2's complement | -A | 0 | 0 | 1 | 0 |
| subtract | B-A | 1 | 0 | 0 | 0 |
| no operation | x | 0 | 0 | 0 | 0 |
| pass A | A | 1 | 1 | 1 | 1 |

