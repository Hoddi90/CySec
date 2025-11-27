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




**Category:** [Scanning / Hardening / Monitoring / Forensics / etc.]  
**Operating System(s):** [Linux / Windows / macOS / Cross-platform]

# <Linux-CLI-Basics-&-Useful-Commands>

**Category:** General Linux CLI / System Usage  
**Operating System(s):** Linux / macOS / WSL

---

## Purpose

A compact reference for essential Linux commands:
- navigating the filesystem  
- reading/writing files  
- permissions  
- copying/moving  
- searching  
- editing  
- pipes and command chaining  
- a few advanced utilities

Useful for daily work, scripting, and troubleshooting.

---

# 1. Navigation

### Go to a directory
```bash
cd folder/
cd ..       # up one level
cd -        # previous directory
cd ~        # home directory
```

### List files
```bash
ls
ls -l       # detailed
ls -a       # include hidden files
ls -lh      # human-readable sizes
```

### Show where you are
```bash
pwd
```

---

# 2. Read / Write Files

### Read a file
```bash
cat file.txt
less file.txt
head file.txt
tail file.txt
tail -f logfile     # live log output
```

### Create or update timestamp
```bash
touch file.txt
```

### Redirect output to a file
```bash
echo "hello" > file.txt     # overwrite
echo "more text" >> file.txt # append
```

### View file type
```bash
file filename
```

---

# 3. Copy / Move / Delete

### Copy
```bash
cp file1 file2
cp -r folder1 folder2
```

### Move / rename
```bash
mv oldname newname
mv file.txt folder/
```

### Delete
```bash
rm file
rm -r folder
```

---

# 4. Permissions (r / w / x)

### Check permissions
```bash
ls -l
```

### Change permissions
```bash
chmod 644 file   # rw-r--r--
chmod 755 script # rwxr-xr-x
chmod +x script  # add execution bit
```

### Change owner
```bash
sudo chown user:group file
sudo chown -R user folder
```

---

# 5. Searching (find / grep)

### Find files by name
```bash
find . -name "*.txt"
```

### Find directories
```bash
find . -type d -name "config"
```

### Find by size
```bash
find . -size +5M
```

### Search inside files
```bash
grep "text" file.txt
grep -R "error" .
grep -Ri "keyword" /etc
```

---

# 6. Pipes & Command Chaining

### Pipe output into another command
```bash
ls -l | grep ".txt"
```

### Count number of matches
```bash
grep -R "TODO" . | wc -l
```

### Sort output
```bash
ls -lh | sort -k5 -n   # sort by size
```

### Head + Grep + Sort example
```bash
ps aux | sort -nrk 3 | head
```

### Find + Grep example
```bash
find . -type f | xargs grep "pattern"
```

### Find big files
```bash
find . -type f -printf "%s %p\n" | sort -n | tail
```

---

# 7. Viewing & Editing Text

### nano editor
```bash
nano file.txt
```

### vim editor
```bash
vim file.txt
```

---

# 8. File Compression & Extraction

### Extract
```bash
tar -xvf file.tar
tar -xzvf file.tar.gz
unzip file.zip
```

### Create archive
```bash
tar -cvf backup.tar folder/
tar -czvf backup.tar.gz folder/
```

---

# 9. System Info & Processes

### System info
```bash
uname -a
df -h
free -h
```

### Processes
```bash
ps aux
top
htop
```

### Kill processes
```bash
kill PID
kill -9 PID
```

---

# 10. Networking (Basics)

### Ping
```bash
ping -c 4 8.8.8.8
```

### Check open ports
```bash
ss -tulnp
```

### DNS lookup
```bash
dig example.com
```

### Download a file
```bash
curl -O https://example.com/file
wget https://example.com/file
```

---

# 11. Useful Quick Commands

### Count lines / words / characters
```bash
wc -l file
wc -w file
wc -c file
```

### Strings from binary
```bash
strings file | grep "keyword"
```

### Hex dump
```bash
xxd file
```

### Check memory + CPU
```bash
top
vmstat
iostat
```

### Check date/time
```bash
date
```

