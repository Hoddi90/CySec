---
tags:
  - Category/Terminology
aliases:
  - Terminoligy
---


**Definition:**  
A buffer overflow is a bug where a program writes more data into a buffer (fixed-size memory region) than it can hold, causing data to spill into adjacent memory and potentially overwrite control data like return addresses.

**Context / Example:**  
- **How/where it’s used:**  
	Common in low-level languages like C/C++ when bounds are not checked (e.g., unsafe string functions). Attackers exploit buffer overflows to crash programs or inject and execute malicious code with the program’s privileges.
- **Concrete example:**  
	A C program uses `gets()` to read user input into a 32-byte stack buffer. An attacker sends 200 bytes: the extra bytes overwrite the saved return address on the stack. When the function returns, execution jumps to attacker-controlled code instead of the legitimate caller.

**Related Concepts:**  
Links to other terms.
- [Related term 1]
- [Related term 2]