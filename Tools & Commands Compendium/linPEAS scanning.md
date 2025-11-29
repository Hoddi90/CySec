---
tags:
  - Category/Tools-Commands
aliases:
  - Tools-Commands
OS:
  - Linux
  - macOS
Type:
  - Scanning
  - Forensics
---

---

## Purpose

- Using linpeas to get a full scan of the system and find possible attack vectors

---

## Installing

The script can be installed from github with curl fx. 

```bash
curl -L https://github.com/peass-ng/PEASS-ng/releases/latest/download/linpeas.sh 
```

## Basic Syntax / Example

Here is a description of the options
```
Checks:
	-a Perform all checks: 1 min of processes, su brute, and extra checks.
	-o Only execute selected checks (system_information,container,cloud,procs_crons_timers_srvcs_sockets,network_information,users_information,software_information,interesting_perms_files,interesting_files,api_keys_regex). Select a comma separated list.
	-s Stealth & faster (don't check some time consuming checks)
	-e Perform extra enumeration
	-r Enable Regexes (this can take from some mins to hours)
	-P Indicate a password that will be used to run 'sudo -l' and to bruteforce other users accounts via 'su'
	-n Do not check hostname & IP in known malicious lists and leaks
	-D Debug mode
Network recon:
	-t Automatic network scan - This option writes to files
	-d <IP/NETMASK> Discover hosts using fping or ping. Ex: -d 192.168.0.1/24
	-p <PORT(s)> -d <IP/NETMASK> Discover hosts looking for TCP open ports (via nc). By default ports 22,80,443,445,3389 and another one indicated by you will be scanned (select 22 if you don't want to add more). You can also add a list of ports. Ex: -d 192.168.0.1/24 -p 53,139
	-i <IP> [-p <PORT(s)>] Scan an IP using nc. By default (no -p), top1000 of nmap will be scanned, but you can select a list of ports instead. Ex: -i 127.0.0.1 -p 53,80,443,8000,8080
	 Notice that if you specify some network scan (options -d/-p/-i but NOT -t), no PE check will be performed
Port forwarding (reverse connection):
	-F LOCAL_IP:LOCAL_PORT:REMOTE_IP:REMOTE_PORT Execute linpeas to forward a port from a your host (LOCAL_IP:LOCAL_PORT) to a remote IP (REMOTE_IP:REMOTE_PORT)
Firmware recon:
	-f </FOLDER/PATH> Execute linpeas to search passwords/file permissions misconfigs inside a folder
Misc:
	-h To show this message
	-w Wait execution between big blocks of checks
	-L Force linpeas execution
	-M Force macpeas execution
	-q Do not show banner
	-N Do not use colours

```

To excecute the full script options -a and -r are the options to select 
```bash
#To output only to console:
./linpeas.sh -a -r


#To output to a file:
./linpeas.sh -a -r > output.txt
#Then read the file later
less -r output.txt
```

From the output, everything that has red text or red text with yellow background is a possible attach vector. 
Most of the things in the scan can be looked at in the [[Privilege escalation handbook]] resource 