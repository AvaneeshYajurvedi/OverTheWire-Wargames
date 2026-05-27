# Bandit Level 5 → Level 6

##  Level Goal

Find the file containing the password inside multiple directories.
The correct file is:

* Human-readable
* Exactly **1033 bytes** in size
* Hidden somewhere in the directory tree

---

##  Step 1: Connect via SSH

Log in using credentials from Level 4:

```
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

---

##  Step 2: Navigate to the Directory

List files:

```
ls
```

### Output:

```id="r2w7qn"
inhere
```

Move into it:

```
cd inhere
```

---

##  Step 3: Analyze the Structure

Inside `inhere`, there are multiple directories:

```
ls
```

### Output:

```
maybehere00
maybehere01
...
maybehere19
```

Checking each manually would be inefficient, so we use a smarter approach.

---

##  Step 4: Use `find` with File Identification

We search for files that are exactly **1033 bytes** and immediately check their type:

```
find . -type f -size 1033c -exec file {} \;
```

### Output:

```
./maybehere07/.file2: ASCII text, with very long lines (1000)
```

This tells us:

* The file is located in `maybehere07`
* It is human-readable (**ASCII text**)

---

##  Step 5: Read the File

```
cat ./maybehere07/.file2
```

### Output:

```
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

---

##  Final Answer

The password for **Bandit Level 6** is:

```
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

---

##  Key Takeaways

* `find` can be combined with `-exec` to perform actions on results.
* The `file` command helps identify readable files quickly.
* Hidden files (like `.file2`) can contain important data.
* Efficient searching saves time and effort.

---

##  Progress

✔ Completed Level 5
➡ Moving to Level 6


