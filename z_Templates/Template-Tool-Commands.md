---
tags:
  - Category/Tools-Commands
aliases:
  - Tools-Commands
OS:
  - Linux
  - Windows
  - macOS
  - Cross-Platform
Type:
  - Scanning
  - Hardening
  - Monitoring
  - Forensics
---

<%*
//prompt for Tool-Name/Command
const name = await tp.system.prompt("Enter Tool-Name/Command");
if (!name) return;
await tp.file.rename(name);
%>


**Category:** [Scanning / Hardening / Monitoring / Forensics / etc.]  
**Operating System(s):** [Linux / Windows / macOS / Cross-platform]

---

## Purpose

- [What it does / when to use it]

---

## Basic Syntax / Example

```bash
[command] [options] [target]
# Example:
[example command]
```

```python
# Example (Python usage)
import subprocess

command = ["nmap", "-sV", "192.168.0.10"]
result = subprocess.run(command, capture_output=True, text=True)

print(result.stdout)

```