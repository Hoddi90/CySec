---
tags:
  - Category/Terminology
aliases:
  - Terminoligy
---


**Definition:**  
The Trusted Computing Base (TCB) is the set of all hardware, software, and controls that must be trusted to enforce a system’s security policy correctly.
If the integrity of the TCB is violated, you can not trust anything !

**Context / Example:**  
- **How/where it’s used:**  
	Used in security design and evaluation to define the minimal part of a system that _must_ be secure. The smaller and simpler the TCB, the easier it is to verify and protect.
- **Concrete example:**  
	On a typical OS, the TCB might include the kernel, low-level device drivers, the login/authentication service, and hardware like the CPU and MMU. If the kernel is compromised (part of the TCB), an attacker can bypass all access control on the system.

**Related Concepts:**  
Links to other terms.
- [Related term 1]
- [Related term 2]