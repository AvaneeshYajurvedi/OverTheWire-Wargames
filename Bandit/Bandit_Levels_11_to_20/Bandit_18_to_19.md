# Bandit Level 18 → Level 19

##  Level Goal

The password for the next level is stored in a file called:

```text
readme
```

However, there is a problem.

Someone modified:

```text
.bashrc
```

which automatically logs users out immediately after login.

The challenge becomes:

> How do we read `readme` without getting kicked out?

---

##  Step 1: Attempt Normal Login

Login normally:

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220
```

Enter password from previous level:

```text
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

Connection closes immediately.

Observation:

```text
Something is executing automatically after login.
```

The level hint explains that `.bashrc` was modified.

Normally:

```text
SSH → Login → Interactive shell opens
```

Here:

```text
SSH → Login → .bashrc executes → Session closes
```

---

##  Step 2: Bypass Interactive Shell

SSH allows running commands directly during login.

Syntax:

```bash
ssh user@host command
```

Instead of opening an interactive shell, SSH executes the command immediately.

First attempt:

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat reamde
```

Mistyped filename:

```text
reamde
```

No useful output.

Correct command:

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```

Enter Bandit18 password.

---

##  Step 3: Retrieve Password

Output:

```text
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

Success.

The command executes before the modified shell configuration can interrupt the session.

---

##  Final Answer

Password for **Bandit Level 19**:

```text
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

---

##  Key Takeaways

- SSH can execute commands directly:

```bash
ssh user@host command
```

- Interactive shells are not always required.
- Shell startup files like `.bashrc` can affect login behavior.
- Understanding how SSH works gives alternative paths when normal access breaks.

---

