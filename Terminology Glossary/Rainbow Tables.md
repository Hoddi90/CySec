---
tags:
  - Category/Terminology
aliases:
  - Terminoligy
---


**Definition:**  
A rainbow table is a precomputed table of hash values used to reverse cryptographic hash functions (typically for passwords) much faster than brute force, by trading storage space for time.

**Context / Example:**  
- **How/where it’s used:**  
	Used in password cracking: an attacker who obtains a database of hashed passwords (e.g., MD5 or SHA-1) can look up each hash in a rainbow table instead of trying every possible password on the fly.
- **Concrete example:**  
	A website stores unsalted MD5 hashes of user passwords. An attacker steals the hash database and uses a public rainbow table for MD5; by matching hashes from the database against the table, they recover many users’ original passwords in minutes.

**Related Concepts:**  
Links to other terms.
- [[Hashing]]
- [[Rainbow Tables]]