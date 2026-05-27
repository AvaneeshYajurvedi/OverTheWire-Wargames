# Bandit Level 7 → Level 8

##  Level Goal

Find the password inside a large file (`data.txt`).
The password is stored next to the word **"millionth"**.

---

##  Step 1: Connect via SSH

Log in using credentials from Level 6:

```
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

---

##  Step 2: Inspect the Files

List directory contents:

```
ls -la
```

### Output:

```
data.txt
```

There is a single large file (~4MB), which likely contains the password.

---

##  Step 3: Analyze the File

Check file type:

```
file data.txt
```

### Output:

```
Unicode text, UTF-8 text
```

So the file is readable—but opening it directly would be inefficient due to its size.

---

##  Step 4: Search Efficiently with `grep`

Instead of scrolling manually, we search for the keyword **"millionth"**:

```
grep "millionth" data.txt
```

### Output:

```
millionth	dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

---

##  Final Answer

The password for **Bandit Level 8** is:

```
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

---

##  Key Takeaways

* `grep` is powerful for searching specific patterns in large files.
* Avoid manual reading when dealing with large datasets.
* Efficiency in CTFs often comes from using the right tool, not more effort.

---

##  Progress

✔ Completed Level 7
➡ Moving to Level 8

---

