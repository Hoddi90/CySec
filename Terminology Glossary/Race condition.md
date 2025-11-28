---
tags:
  - Category/Terminology
aliases:
  - Terminoligy
---


**Definition:**  
A race condition is a bug that occurs when a system’s behavior depends on the timing or interleaving of concurrent operations, so the outcome becomes unpredictable and can be manipulated or differs run-to-run.

**Context / Example:**  
- **How/where it’s used:**  
Appears in multithreaded programs, OS kernels, and concurrent systems where multiple processes/threads or users access shared resources (files, memory, variables) without proper synchronization. Attackers can exploit race conditions to bypass checks or corrupt data.
- **Concrete example:**  
Two threads update a shared counter `balance` without locking. Both read `balance = 100`, then each adds 10 and writes back 110. The final value is 110 instead of 120 because the operations overlapped—this lost update is caused by a race condition.

**Related Concepts:**  
Links to other terms.
- [[TOCTOU]]
- [Related term 2]