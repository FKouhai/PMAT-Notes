# Advanced Analysis

- ## Advanced Static Analysis

Its the use of decompilers and disassemblers to see how the binary acts on a low level

- ## Advanced Dynamic Analysis

Its the use of a debugger, to investigate how the program executes

- ## Asembly Instructions

Asembly is a low level language that translates the patterns of CPU code into human readable code, using cutter in windows allows you to see the insides of the binary
![[Pasted image 20211227115048.png]]

The decompiler tab, tries to recreate the code of the program

For a binary to run on x86_64 cpus, we have

   - CPU Instructions
   		There are 3 types, arithmetic, control flow and data movement, in little endian which is what x86 is based on the syntax is verb dst, src
		mov edx,eax
		jmp memLoc (jnz == jump if not zero)
		sub
	- STACK
		The stack grows downwards
		push 0,string,12 (this will push those values into the stack)
		pop 12 (this will pop out of the stack the value 12) 
		call (calls a function, its location gets saved in the ebp)
		ret (returns to a function, usually main)
	- MEMORY REGISTERS
		eax
		edx
		ebx
		esp
		ebp
		eip
		
