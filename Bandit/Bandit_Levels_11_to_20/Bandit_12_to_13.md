# Bandit Level 12 → Level 13

##  Level Goal

The password for the next level is stored inside a file that contains a **hex dump**.

The challenge requires repeatedly decoding and extracting nested compressed files until reaching the final plaintext password.

---

##  Step 1: Connect via SSH

Login using credentials from the previous level:

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

---

##  Step 2: Inspect the File

List available files:

```bash
ls
```

Output:

```text
data.txt
```

View file contents:

```bash
cat data.txt
```

Output begins:

```text
00000000: 1f8b 0808 ...
```

The file appears to be a **hex dump**.

---

##  Step 3: Create a Working Directory

Bandit home directories are read-only.

Create a temporary workspace:

```bash
mkdir /tmp/avii_bandit12
cd /tmp/avii_bandit12
```

Copy the file:

```bash
cp ~/data.txt .
```

---

##  Step 4: Reverse the Hex Dump

Convert hex back into binary:

```bash
xxd -r data.txt > data.bin
```

Check file type:

```bash
file data.bin
```

Output:

```text
gzip compressed data
```

---

##  Step 5: Begin Extracting Layers

### Layer 1 — Gzip

Rename:

```bash
mv data.bin data.gz
```

Extract:

```bash
gunzip data.gz
```

Check type:

```bash
file data
```

Output:

```text
bzip2 compressed data
```

---

### Layer 2 — Bzip2

Rename:

```bash
mv data data.bz2
```

Extract:

```bash
bunzip2 data.bz2
```

Check:

```bash
file data
```

Output:

```text
gzip compressed data
```

---

### Layer 3 — Gzip Again

```bash
mv data data.gz
gunzip data.gz
```

Check:

```bash
file data
```

Output:

```text
POSIX tar archive
```

---

### Layer 4 — Tar Archive

Extract:

```bash
tar xf data
```

New file:

```text
data5.bin
```

Check:

```bash
file data5.bin
```

Output:

```text
POSIX tar archive
```

Extract:

```bash
tar xf data5.bin
```

New file:

```text
data6.bin
```

---

### Layer 5 — Bzip2 Again

Check:

```bash
file data6.bin
```

Output:

```text
bzip2 compressed data
```

Rename:

```bash
mv data6.bin data6.bz2
```

Extract:

```bash
bunzip2 data6.bz2
```

Check:

```bash
file data6
```

Output:

```text
POSIX tar archive
```

Extract:

```bash
tar xf data6
```

New file:

```text
data8.bin
```

---

### Layer 6 — Final Gzip

Check:

```bash
file data8.bin
```

Output:

```text
gzip compressed data
```

Rename:

```bash
mv data8.bin data8.gz
```

Extract:

```bash
gunzip data8.gz
```

Check:

```bash
file data8
```

Output:

```text
ASCII text
```

---

##  Step 6: Retrieve Password

Read final file:

```bash
cat data8
```

Output:

```text
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

---

##  Final Answer

Password for **Bandit Level 13**:

```text
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

---

##  Key Takeaways

- `xxd -r` reverses hex dumps into binary.
- `file` is one of the most valuable reconnaissance tools.
- Compression formats can be nested repeatedly.
- Temporary directories (`/tmp`) are critical when home directories are read-only.
- When stuck, identify file types before acting.

---
