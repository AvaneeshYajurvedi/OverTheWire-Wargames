# Bandit Level 6 → Level 7

##  Level Goal

Find a file somewhere on the system with the following properties:

* Owned by user **bandit7**
* Belongs to group **bandit6**
* Exactly **33 bytes** in size

---

##  Step 1: Connect via SSH

Log in using credentials from Level 5:

```
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

---

##  Step 2: Inspect the Home Directory

```
ls -la
```

### Output:

```
.bashrc
.profile
...
```

Nothing useful here.
This means the file is **not in the home directory**—we need to search the entire system.

---

##  Step 3: Search the Entire Filesystem

We use `find` with multiple filters:

```
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

### Breakdown:

* `/` → search from root (entire system)
* `-type f` → regular files only
* `-user bandit7` → owned by bandit7
* `-group bandit6` → group is bandit6
* `-size 33c` → exactly 33 bytes
* `2>/dev/null` → suppress permission denied errors

---

##  Step 4: Locate the File

### Output:

```
/var/lib/dpkg/info/bandit7.password
```

---

##  Step 5: Read the File

```
cat /var/lib/dpkg/info/bandit7.password
```

### Output:

```
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

---

##  Final Answer

The password for **Bandit Level 7** is:

```
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

---

##  Key Takeaways

* `find /` allows searching the entire filesystem.
* Combine multiple filters (`-user`, `-group`, `-size`) for precision.
* Redirect errors with `2>/dev/null` to keep output clean.
* System-wide searches are essential in real-world scenarios.

---

##  Progress

✔ Completed Level 6
➡ Moving to Level 7

---

