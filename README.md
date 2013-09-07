SM-Assembler
============

An assembler for the Simple Machine

- supports all the commands including the extensions
- variable declarations
- labels for JMP statements
- comments and only comment lines

variables are declared in hex without the leading 0x <br>
ex var1=5F3

labels are declared on a line that you wish to associate it with. ex: <br>
mylabelvar: ADD var1 <br>
and can be used like variables: JMP mylabelvar

To run
======

assembler inputfile [-s] [path to simulator]

outputs the assembled code to stdout with the assembly language code
commented out to the right of the machine language 

if the -s and simulator path are given it outputs the simulator output
of the assembled machine language with the machine and assembly language
commented out to the right of the memory locations

Example program:
================

LOAD val2 # load value stored in val2 <br>
SUB val1 <br>
MVAC <br>
JLT loadval2 # jump to the label loadval2 (line 8) <br>
LOAD val1 <br>
STORE larger <br>
JMP halt <br>
loadval2: LOAD val2 # declare a label loadval2 to point to this line <br>
STORE larger <br>
halt:HALT <br>
\# variable declarations <br>
val1=1B0 <br>
val2=2A <br>
larger=0 <br>

- - - - - - - - - 
would ouput 
- - - - - - - - - 

0x100b # LOAD val2 # load value stored in val2 <br>
0x900a # SUB val1 <br>
0x4000 # MVAC <br>
0x6007 # JLT loadval2 # jump to the label loadval2 (line 8) <br>
0x100a # LOAD val1 <br>
0x200c # STORE larger <br>
0x7009 # JMP halt <br>
0x100b # loadval2: LOAD val2 # declare a label loadval2 to point to this line <br>
0x200c # STORE larger <br>
0x0000 # halt:HALT <br>
\# variable declarations <br>
0x01B0 # val1=1B0 <br>
0x002A # val2=2A <br>
0x0000 # larger=0 <br>

- - - - - - - - 
if run through the simulator with: assembler largerprogram -s pathtosimulator <br>
would output 
- - - - - - - - 

sim: INPUT FILE = /tmp/assembler.sBgmRO <br>
******* BEFORE SIMULATION ******** <br>
__memory[0]	= 0x100b #--# 0x100b # LOAD val2 # load value stored in val2 <br>
__memory[1]	= 0x900a #--# 0x900a # SUB val1 <br>
__memory[2]	= 0x4000 #--# 0x4000 # MVAC <br>
__memory[3]	= 0x6007 #--# 0x6007 # JLT loadval2 # jump to the label loadval2 (line 8) <br>
__memory[4]	= 0x100a #--# 0x100a # LOAD val1 <br>
__memory[5]	= 0x200c #--# 0x200c # STORE larger <br>
__memory[6]	= 0x7009 #--# 0x7009 # JMP halt <br>
__memory[7]	= 0x100b #--# 0x100b # loadval2: LOAD val2 # declare a label loadval2 to point to this line <br>
__memory[8]	= 0x200c #--# 0x200c # STORE larger <br>
__memory[9]	= 0x0000 #--# 0x0000 # halt:HALT <br>
__memory[10]	= 0x01b0 #--# 0x01B0 # val1=1B0 <br>
__memory[11]	= 0x002a #--# 0x002A # val2=2A <br>
__memory[12]	= 0x0000 #--# 0x0000 # larger=0 <br>
8 instructions executed. <br>
******* AFTER SIMULATION ******** <br>
__memory[0]	= 0x100b #--# 0x100b # LOAD val2 # load value stored in val2 <br>
__memory[1]	= 0x900a #--# 0x900a # SUB val1 <br>
__memory[2]	= 0x4000 #--# 0x4000 # MVAC <br>
__memory[3]	= 0x6007 #--# 0x6007 # JLT loadval2 # jump to the label loadval2 (line 8) <br>
__memory[4]	= 0x100a #--# 0x100a # LOAD val1 <br>
__memory[5]	= 0x200c #--# 0x200c # STORE larger <br>
__memory[6]	= 0x7009 #--# 0x7009 # JMP halt <br>
__memory[7]	= 0x100b #--# 0x100b # loadval2: LOAD val2 # declare a label loadval2 to point to this line <br>
__memory[8]	= 0x200c #--# 0x200c # STORE larger <br>
__memory[9]	= 0x0000 #--# 0x0000 # halt:HALT <br>
__memory[10]	= 0x01b0 #--# 0x01B0 # val1=1B0 <br>
__memory[11]	= 0x002a #--# 0x002A # val2=2A <br>
__memory[12]	= 0x01b0 #--# 0x0000 # larger=0 <br>

