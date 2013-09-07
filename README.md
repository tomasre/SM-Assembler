SM-Assembler
============

An assembler for the Simple Machine

- supports all the commands including the extensions
- variable declarations
- labels for JMP statements
- comments and only comment lines

variables are declared in hex without the leading 0x
ex var1=5F3

labels are declared on a line that you wish to associate it with. ex:
mylabelvar: ADD var1
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

LOAD val2 # load value stored in val2
SUB val1
MVAC
JLT loadval2 # jump to the label loadval2 (line 8)
LOAD val1
STORE larger
JMP halt
loadval2: LOAD val2 # declare a label loadval2 to point to this line
STORE larger
halt:HALT
# - - - - - - variable declarations
val1=1B0
val2=2A
larger=0

- - - - - - - - - 
would ouput 
- - - - - - - - - 

0x100b # LOAD val2 # load value stored in val2
0x900a # SUB val1
0x4000 # MVAC
0x6007 # JLT loadval2 # jump to the label loadval2 (line 8)
0x100a # LOAD val1
0x200c # STORE larger
0x7009 # JMP halt
0x100b # loadval2: LOAD val2 # declare a label loadval2 to point to this line
0x200c # STORE larger
0x0000 # halt:HALT
# - - - - - - variable declarations
0x01B0 # val1=1B0
0x002A # val2=2A
0x0000 # larger=0

- - - - - - - - 
if run through the simulator with: assembler largerprogram -s pathtosimulator
would output 
- - - - - - - - 

sim: INPUT FILE = /tmp/assembler.sBgmRO
******* BEFORE SIMULATION ********
__memory[0]	= 0x100b #--# 0x100b # LOAD val2 # load value stored in val2
__memory[1]	= 0x900a #--# 0x900a # SUB val1
__memory[2]	= 0x4000 #--# 0x4000 # MVAC
__memory[3]	= 0x6007 #--# 0x6007 # JLT loadval2 # jump to the label loadval2 (line 8)
__memory[4]	= 0x100a #--# 0x100a # LOAD val1
__memory[5]	= 0x200c #--# 0x200c # STORE larger
__memory[6]	= 0x7009 #--# 0x7009 # JMP halt
__memory[7]	= 0x100b #--# 0x100b # loadval2: LOAD val2 # declare a label loadval2 to point to this line
__memory[8]	= 0x200c #--# 0x200c # STORE larger
__memory[9]	= 0x0000 #--# 0x0000 # halt:HALT
__memory[10]	= 0x01b0 #--# 0x01B0 # val1=1B0
__memory[11]	= 0x002a #--# 0x002A # val2=2A
__memory[12]	= 0x0000 #--# 0x0000 # larger=0
8 instructions executed.
******* AFTER SIMULATION ********
__memory[0]	= 0x100b #--# 0x100b # LOAD val2 # load value stored in val2
__memory[1]	= 0x900a #--# 0x900a # SUB val1
__memory[2]	= 0x4000 #--# 0x4000 # MVAC
__memory[3]	= 0x6007 #--# 0x6007 # JLT loadval2 # jump to the label loadval2 (line 8)
__memory[4]	= 0x100a #--# 0x100a # LOAD val1
__memory[5]	= 0x200c #--# 0x200c # STORE larger
__memory[6]	= 0x7009 #--# 0x7009 # JMP halt
__memory[7]	= 0x100b #--# 0x100b # loadval2: LOAD val2 # declare a label loadval2 to point to this line
__memory[8]	= 0x200c #--# 0x200c # STORE larger
__memory[9]	= 0x0000 #--# 0x0000 # halt:HALT
__memory[10]	= 0x01b0 #--# 0x01B0 # val1=1B0
__memory[11]	= 0x002a #--# 0x002A # val2=2A
__memory[12]	= 0x01b0 #--# 0x0000 # larger=0

