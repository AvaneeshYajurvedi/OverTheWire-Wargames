# Bandit Level 19 → Level 20

##  Level Goal

There is a file named:

```text
bandit20-do
```

The challenge is to figure out how to use it to retrieve the password for the next level.

---

##  Step 1: Login

Connect using the password from the previous level:

```bash
ssh bandit19@bandit.labs.overthewire.org -p 2220
```

Login successful:

```text
bandit19@bandit:~$
```

---

##  Step 2: Check Available Files

List files:

```bash
ls
```

Output:

```text
bandit20-do
```

Interesting.

Only one file exists.

---

##  Step 3: Test the Binary

Try running it:

```bash
./bandit20-do ls
```

Output:

```text
bandit20-do
```

The binary executes commands.

That means it likely runs commands with elevated permissions.

---

##  Step 4: Explore Accessible Password Files

Check password directory:

```bash
./bandit20-do ls /etc/bandit_pass
```

Output:

```text
bandit0
bandit1
bandit2
...
bandit20
...
```

Interesting.

The binary can access protected locations.

---

##  Step 5: First Attempt (Mistake)

Attempt:

```bash
./bandit20 cat /etc/bandit_pass/bandit20
```

Output:

```text
-bash: ./bandit20: No such file or directory
```

Problem:

```text
bandit20
```

does not exist.

The executable is:

```text
bandit20-do
```

---

##  Step 6: Execute Correct Command

Run:

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

Output:

```text
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

Success.

The binary executed the command using Bandit20 privileges.

---

##  Final Answer

Password for **Bandit Level 20**:

```text
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

---

##  Key Takeaways

- Linux binaries can execute commands with different permissions.
- Always inspect provided executables carefully.
- Testing binaries reveals their behavior.
- Small mistakes matter:

Wrong:

```bash
./bandit20
```

Correct:

```bash
./bandit20-do
```

- Privilege escalation concepts appear frequently in cybersecurity.

---

