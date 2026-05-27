# Bandit Level 1 → Level 2

##  Level Goal

Retrieve the password for the next level.
The challenge introduces a tricky filename: a single dash (`-`).

---

##  Step 1: Connect via SSH

We log in using the credentials obtained from the previous level:

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

After entering the password from Level 0, access is granted.

---

##  Step 2: List Files

Check the contents of the home directory:

```bash
ls
```

### Output:

```
-
```

At first glance, this looks… suspiciously minimal.
A file named `-` isn’t just unusual—it’s problematic.

---

##  Understanding the Problem

In Linux, `-` is often treated as **standard input (stdin)** rather than a filename.
So if you try:

```bash
cat -
```

…it won’t read the file—it will wait for input instead.

---

##  Step 3: Access the File Correctly

To explicitly refer to the file, we specify its path:

```bash
cat ./-
```

* `./` tells the shell: *“this is a file in the current directory”*
* This avoids confusion with stdin

---

##  Step 4: Read the Password

### Output:

```
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

---

##  Final Answer

The password for **Bandit Level 2** is:

```
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

---

##  Key Takeaways

* Filenames like `-` can conflict with shell conventions.
* Prefixing with `./` forces the shell to treat it as a file.
* Not everything in Linux is straightforward—sometimes the challenge is the *name itself*.

---

##  Progress

✔ Completed Level 1
➡ Moving to Level 2

---



