---
tags:
  - Category/Terminology
aliases:
  - Terminoligy
---


**Definition:**  
Hashing is the process of transforming input data of arbitrary size into a fixed-size output (a hash value) using a hash function, in a way that is fast to compute and hard to reverse.

**Context / Example:**  
- **How/where it’s used:**  
	Used for data integrity checks, password storage, digital signatures, and indexing. In security, passwords are stored as hashes instead of plain text so the original password is not directly revealed if the database leaks.
- **Concrete example:**  
	When a user creates an account, the server runs their password through a hash function like SHA-256 or bcrypt and stores only the hash. Later, when the user logs in, the server hashes the entered password and compares it to the stored hash to verify the user without ever storing the actual password.

**Related Concepts:**  
Links to other terms.
- [[Salting]]
- [[Rainbow Tables]]