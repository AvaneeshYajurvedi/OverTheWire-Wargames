# Bandit Level 9 → Level 10

##  Level Goal

Find the password hidden inside a **binary file** (`data.txt`).
The password is located near multiple `=` characters.

---

##  Step 1: Connect via SSH

Log in using credentials from Level 8:

```
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

---

##  Step 2: Inspect the Files

```
ls -la
```

### Output:

```
data.txt
```

---

##  Step 3: Initial Attempt

Trying to search directly:

```
grep "=" data.txt
```

### Output:

```
binary file matches
```

The file is binary, so `grep` cannot display readable matches directly.

---

##  Step 4: Extract Readable Strings

We use the `strings` command to extract human-readable text:

```
strings data.txt | grep "="
```

### Output (excerpt):

```
========== the
2========== password
========== is
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

---

##  Step 5: Identify the Password

From the readable output, the line clearly reveals:

```
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

---

##  Final Answer

The password for **Bandit Level 10** is:

```
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

---

##  Key Takeaways

* Binary files cannot be read directly using `cat` or `grep`.
* `strings` extracts readable sequences from binary data.
* Combining `strings` with `grep` helps filter meaningful information.
* Not all data is meant to be read—sometimes you extract only what matters.

---

##  Progress

✔ Completed Level 9
➡ Moving to Level 10

---


