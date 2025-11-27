---
tags:
  - Category/Terminology
aliases:
  - Terminoligy
---


**Definition:**  
A Real-Time Operating System (RTOS) is an operating system designed to guarantee that critical tasks complete within strict timing deadlines, providing predictable (deterministic) response rather than maximum throughput.

**Context / Example:**  
- **How/where it’s used:**  
	Used in embedded and cyber-physical systems where timing is safety- or mission-critical, such as industrial controllers, automotive ECUs, medical devices, and avionics. The RTOS scheduler ensures high-priority tasks meet their deadlines.
- **Concrete example:**  
	In an anti-lock braking system (ABS) in a car, an RTOS runs tasks that read wheel sensors and adjust braking pressure every few milliseconds. Missing a deadline could cause the brakes to react too late, so the RTOS guarantees that the control loop always runs on time.

**Related Concepts:**  
Links to other terms.
- Embedded system