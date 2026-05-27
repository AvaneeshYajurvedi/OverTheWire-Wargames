# Bandit Level 3 → Level 4

##  Level Goal

Retrieve the password for the next level.
This level introduces **hidden files** inside a directory.

---

##  Step 1: Connect via SSH

Log in using credentials from Level 2:

```bash id="k9d2pl"
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

---

##  Step 2: Explore the Directory

List files in the home directory:

```bash id="c3x8mn"
ls
```

### Output:

```id="z7q2vd"
inhere
```

There’s a directory named `inhere`. Let’s move into it:

```bash id="w1n5ra"
cd inhere
```

---

##  Step 3: Look for Hidden Files

Running a normal `ls` shows nothing:

```bash id="h6j3lp"
ls
```

No output. Suspicious.

Hidden files in Linux start with a `.` and aren’t shown by default.
So we use:

```bash id="p8v2xt"
ls -la
```

### Output:

```id="m4r9qs"
.
..
...Hiding-From-You
```

There it is—a file literally trying to stay invisible.

---

##  Step 4: Read the Hidden File

```bash id="u2f8kc"
cat ...Hiding-From-You
```

### Output:

```id="b5x7ne"
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

---

##  Final Answer

The password for **Bandit Level 4** is:

```id="d1n8wo"
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

---

##  Key Takeaways

* Hidden files start with a `.` and require `ls -a` or `ls -la` to be visible.
* Always question empty output—sometimes it’s hiding something.
* Directory exploration is a core skill in Linux and CTFs.

---

##  Progress

✔ Completed Level 3
➡ Moving to Level 4

---


