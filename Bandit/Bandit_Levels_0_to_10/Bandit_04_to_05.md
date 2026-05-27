# Bandit Level 4 → Level 5

##  Level Goal

Find the correct file among multiple files and retrieve the password.
Only one file contains **human-readable text**—the rest are binary/data.

---

##  Step 1: Connect via SSH

Log in using credentials from Level 3:

```
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

---

##  Step 2: Navigate to the Directory

List files in the home directory:

```
ls
```

### Output:

```
inhere
```

Move into it:

```
cd inhere
```

---

##  Step 3: Inspect Files

List all files:

```
ls -la
```

### Output (simplified):

```
-file00
-file01
...
-file09
```

Each file starts with `-`, which can confuse commands (treated as options).

---

##  Initial Attempt

Trying to read directly:

```
cat -file00
```

Results in an error because `-f` is interpreted as an option.

---

##  Step 4: Identify the Correct File

We use the `file` command to check file types:

```
file ./*
```

### Output (important part):

```
./-file07: ASCII text
```

Only `-file07` contains readable text. The rest are binary (`data`).

---

##  Step 5: Read the Correct File

To safely read a file starting with `-`, we use `./`:

```
cat ./-file07
```

### Output:

```
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

---

##  Final Answer

The password for **Bandit Level 5** is:

```
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

---

##  Key Takeaways

* Files starting with `-` must be accessed carefully using `./` or `--`.
* The `file` command helps identify file types quickly.
* Not all files are meant to be read—find the one that *makes sense*.

---

##  Progress

✔ Completed Level 4
➡ Moving to Level 5

---


