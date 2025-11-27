---
tags:
  - Category/Terminology
aliases:
  - Terminoligy
---


**Definition:**  
POSIX (Portable Operating System Interface) is a family of IEEE/ISO standards that define a common API and behavior for operating systems, mainly based on Unix, to improve portability of applications across different systems.

**Context / Example:**  
- **How/where it’s used:**  
	Used as a compatibility standard so programs written for one POSIX-compliant OS (e.g., Linux, macOS, many [[Unix]] variants) can be recompiled and run on another with minimal changes. It specifies things like process control, file I/O, signals, threads, and shells.
- **Concrete example:**  
	A C program that uses POSIX system calls like `fork()`, `execve()`, `open()`, and `read()` can be compiled and run on both Linux and macOS because both provide the POSIX-defined behavior for these calls.

**Related Concepts:**  
Links to other terms.
- [[Unix]]
- [Related term 2]