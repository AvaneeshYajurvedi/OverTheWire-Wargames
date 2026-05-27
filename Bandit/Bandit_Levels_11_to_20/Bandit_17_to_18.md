# Bandit Level 17 → Level 18

##  Level Goal

There are two files in the home directory:

```text
passwords.old
passwords.new
```

Only **one line** differs between them.

The changed line inside `passwords.new` is the password for the next level.

---

##  Step 1: Login Using SSH Key

Login using the private SSH key obtained in the previous level:

```bash
ssh -i sshkey1.private bandit17@bandit.labs.overthewire.org -p 2220
```

Login successful:

```text
bandit17@bandit:~$
```

---

##  Step 2: Check Available Files

List files:

```bash
ls
```

Output:

```text
passwords.new
passwords.old
```

Two files are present.

The level description hints that only one line changed.

At first, opening both files manually is possible:

```bash
cat passwords.old
cat passwords.new
```

But both files contain many lines.

Manual comparison would be painful.

---

##  Step 3: Use `diff`

Linux provides a built-in utility specifically designed for comparing files:

```bash
diff passwords.old passwords.new
```

Output:

```text
42c42
< 390zFj2NETFVZkqYw8UEFdN6h40oGVtT
---
> x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

Explanation:

```text
42c42
```

Means:

- Line 42 in `passwords.old`
- Was changed in line 42 of `passwords.new`

Old value:

```text
390zFj2NETFVZkqYw8UEFdN6h40oGVtT
```

New value:

```text
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

The challenge states the changed line inside `passwords.new` is the next password.

---

##  Final Answer

Password for **Bandit Level 18**:

```text
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

---

##  Key Takeaways

- `diff` compares two files line by line.
- Linux utilities save huge amounts of manual effort.
- Reading challenge instructions carefully often reveals exactly which tool to use.
- Automation beats manual searching.

Useful syntax:

```bash
diff file1 file2
```

---

