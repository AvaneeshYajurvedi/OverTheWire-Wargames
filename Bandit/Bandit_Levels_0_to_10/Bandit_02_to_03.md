# Bandit Level 2 → Level 3

##  Level Goal

Retrieve the password for the next level.
This level introduces filenames containing **spaces**, which require special handling in the shell.

---

##  Step 1: Connect via SSH

Log in using the credentials obtained from Level 1:

```
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

After entering the password, we gain access to the system.

---

##  Step 2: List Files

Check the contents of the home directory:

```
ls
```

### Output:

```
--spaces in this filename--
```

Now this is where things get tricky.
The filename contains **spaces**, which the shell interprets as separators between arguments.

---

##  Understanding the Problem

If we try:

```bash id="k2f3nm"
cat --spaces in this filename--
```

The shell interprets it as multiple arguments:

* `--spaces`
* `in`
* `this`
* `filename--`

This leads to errors because the file is not being referenced correctly.

---

##  Step 3: Access the File Properly

To handle spaces in filenames, we wrap the name in quotes and use `--` to signal the end of options:

```
cat -- "--spaces in this filename--"
```

* `--` tells the command: *“no more options follow”*
* Quotes ensure the filename is treated as a single argument

---

##  Step 4: Retrieve the Password

### Output:

```
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

---

##  Final Answer

The password for **Bandit Level 3** is:

```
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

---

##  Key Takeaways

* Filenames with spaces must be:

  * Wrapped in quotes `" "`
  * Or escaped using `\`
* The `--` operator is useful to stop option parsing in commands.
* The shell doesn’t forgive ambiguity—be precise.

---

##  Progress

✔ Completed Level 2
➡ Moving to Level 3

---



