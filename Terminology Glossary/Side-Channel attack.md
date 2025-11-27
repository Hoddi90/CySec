---
tags:
  - Category/Terminology
aliases:
  - Terminoligy
---


**Definition:**  
A side-channel attack is a technique where an attacker infers secrets (like cryptographic keys) by measuring _indirect_ information from a system, such as timing, power use, electromagnetic emissions, or cache behavior, instead of breaking the algorithm itself.

**Context / Example:**  
- **How/where it’s used:**  
	Used to attack implementations of cryptography or secure code on CPUs, smart cards, phones, or cloud VMs by observing how the system behaves while it processes secret data.
- **Concrete example 1:**  
	An attacker measures how long a server takes to perform an RSA decryption; tiny timing differences (caused by different key bits) are collected over many requests, then analyzed to recover the private key.
- **Concrete example 2:**  
	An attacker places a probe near a smart card that performs AES encryption and measures its power consumption while it encrypts many chosen plaintexts. By analyzing patterns in the power traces (differential power analysis), the attacker can recover the secret AES key without ever breaking the algorithm itself.

**Related Concepts:**  
Links to other terms.
- [Related term 1]
- [Related term 2]