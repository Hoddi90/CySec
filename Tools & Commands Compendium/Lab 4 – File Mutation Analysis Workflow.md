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

---

# Lab 4 – Workflow (No auditd, No Windows ADS Issues)
This workflow ensures correct CREATED / DELETED / CHANGED lists while avoiding all Windows-generated NTFS `:Zone.Identifier` and `:Zone - Copy.Identifier` artifacts.

---

# 0. Critical Rules Before Starting
1. **Never copy forest directories using Windows Explorer.**  
   This creates NTFS ADS files like:  
   - `file.txt:Zone.Identifier`
   - `file.txt:Zone - Copy.Identifier`  
   These cause hundreds of false CREATED files.

2. **Only copy using WSL/Linux commands** such as `cp -r`.

3. **Never run the mutation binary twice** on the same forest.  
   Always mutate only the `forest_after` folder.

---

# 1. Prepare Two Clean Forest Copies

Unzip the original lab archive **inside WSL**, not Windows Explorer.

Example:

```bash
unzip forest.zip -d lab4
```

Inside `lab4/` you will see something like:

```
forest_4d666854/
forest_worker_linux
```

Now make two **Linux-only copies**:

```bash
cp -r lab4/forest_4d666854 forest_original
cp -r lab4/forest_4d666854 forest_after
```

Resulting directory structure:

```
forest_original/
forest_after/
forest_worker_linux
```

Both folders are identical and free of Windows ADS pollution.

---

# 2. Remove Windows ADS Files (Safety Step)

If the ZIP ever touched Windows Explorer, ADS files may still exist.

Clean both folders:

```bash
find forest_original -type f -name "*:Zone*" -delete
find forest_after    -type f -name "*:Zone*" -delete
```

This removes:
- `:Zone.Identifier`
- `:Zone - Copy.Identifier`
- any similar ADS copies

---

# 3. Run the Mutation Binary Once

Copy the worker binary into `forest_after` if needed:

```bash
cp forest_worker_linux forest_after/
```

Run it:

```bash
cd forest_after
chmod +x forest_worker_linux
./forest_worker_linux
```

This mutates only `forest_after`.  
`forest_original` stays untouched.

---

# 4. Verify File Counts

Back in the parent folder:

```bash
echo ORIGINAL:
find forest_original -type f | grep -v ":Zone" | wc -l

echo AFTER:
find forest_after -type f | grep -v ":Zone" | wc -l
```

Expected:

- ORIGINAL → **1004 files**
- AFTER → **1012 files**

---

# 5. Build BEFORE and AFTER File Lists (Relative Paths)

```bash
find forest_original -type f -printf '%P\n' \
    | grep -v ":Zone" \
    | sort > before.txt

find forest_after -type f -printf '%P\n' \
    | grep -v ":Zone" \
    | sort > after.txt
```

Preview:

```bash
head before.txt
head after.txt
```

Should look like:

```
aahbptju/file1.txt
aahbptju/file2.txt
...
```

No extra folders, no ADS suffixes.

---

# 6. Compute CREATED and DELETED

### CREATED (files only in AFTER)

```bash
comm -13 before.txt after.txt > created.txt
```

Expected count: **8**

---

### DELETED (files only in ORIGINAL)

```bash
comm -23 before.txt after.txt > deleted.txt
```

Expected count: **10**

---

# 7. Compute CHANGED Files (Using SHA1)

### Compute checksums

```bash
find forest_original -type f -exec sha1sum {} + \
    | sed 's#forest_original/##' \
    | grep -v ":Zone" \
    | sort > before_sha.txt

find forest_after -type f -exec sha1sum {} + \
    | sed 's#forest_after/##' \
    | grep -v ":Zone" \
    | sort > after_sha.txt
```

### Extract unchanged files

```bash
comm -12 before_sha.txt after_sha.txt | cut -d' ' -f3 > unchanged.txt
```

### Extract files present in both trees

```bash
comm -12 before.txt after.txt > common.txt
```

### CHANGED = common - unchanged

```bash
grep -Fvxf unchanged.txt common.txt > changed.txt
```

Expected count: **10**

---

# 8. Final Cleanup (Optional)

If assignment forbids certain files by name (e.g., “do not include me”):

```bash
for f in created.txt deleted.txt changed.txt; do
    sed -i '/Zone/d' "$f"
    sed -i '/do not include me/d' "$f"
done
```

---

# 9. Format for Canvas Submission

Use this format:

```
SEED;
DELETED: file1,file2,file3,...
CHANGED: file1,file2,...
CREATED: file1,file2,...
```

Make sure:
- No spaces around commas.
- Relative paths only.
- No Zone.Identifier junk.

---

# Final Expected Results

- **DELETED → 10 files**
- **CHANGED → 10 files**
- **CREATED → 8 files**

If your counts match this, the Verifier will return:
- Deleted correct: 10/10  
- Changed correct: 10/10  
- Added correct: 8/8  

