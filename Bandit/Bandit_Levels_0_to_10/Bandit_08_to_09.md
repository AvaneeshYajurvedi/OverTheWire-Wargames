# Bandit Level 8 → Level 9

##  Level Goal

Find the password inside `data.txt`.
The correct line is the **only one that appears once**—all others are repeated.

---

##  Step 1: Connect via SSH

Log in using credentials from Level 7:

```
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

---

##  Step 2: Inspect the Files

List directory contents:

```
ls
```

### Output:

```
data.txt
```

---

##  Step 3: Understand the Challenge

The file contains many repeated lines, but:

* Only **one line is unique**
* That unique line is the password

---

##  Step 4: Filter Unique Lines

We use a pipeline of commands:

```
cat data.txt | sort | uniq -u
```

### Breakdown:

* `cat data.txt` → outputs file content
* `sort` → groups identical lines together
* `uniq -u` → shows only lines that appear **once**

---

##  Step 5: Retrieve the Password

### Output:

```
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

---

##  Final Answer

The password for **Bandit Level 9** is:

```
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

---

##  Key Takeaways

* `sort` is often required before using `uniq` effectively.
* `uniq -u` filters out everything except unique lines.
* Piping commands (`|`) allows chaining tools for powerful data processing.
* Sometimes the answer isn’t hidden—it’s just the only thing left standing.

---

##  Progress

✔ Completed Level 8
➡ Moving to Level 9

---


