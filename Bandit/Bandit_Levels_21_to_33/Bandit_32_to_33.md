# OverTheWire Bandit Level 32 → Level 33

## Objective

Bandit32 introduces a restricted shell:

```text
UPPERCASE SHELL
```

The shell automatically converts commands to uppercase, making normal Linux commands unusable.

Goal:

Retrieve the Bandit33 password.

---

## Step 1: Login

Connect normally:

```bash
ssh bandit32@bandit.labs.overthewire.org -p 2220
```

Enter password from previous level:

```text
3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
```

Login successful.

Output:

```text
WELCOME TO THE UPPERCASE SHELL
>>
```

Interesting.

---

## Step 2: Test Commands

Try:

```bash
ls
```

Output:

```text
sh: 1: LS: Permission denied
```

Problem:

The shell converts everything into uppercase.

Command entered:

```bash
ls
```

Actually becomes:

```bash
LS
```

Linux commands are case-sensitive.

Need another approach.

---

## Step 3: Escape Restricted Shell

Try:

```bash
$0
```

Output:

```bash
$
```

Success.

Explanation:

```bash
$0
```

references the current shell executable.

Executing it spawns a normal shell.

Restricted shell bypassed.

---

## Step 4: Verify Shell Access

Run:

```bash
ls -la
```

Output:

```text
.bashrc
.profile
uppershell
```

Now commands work normally.

---

## Step 5: Check Current User

Run:

```bash
whoami
```

Output:

```text
bandit33
```

Interesting.

Privileges already switched.

---

## Step 6: Retrieve Password

Read password file:

```bash
cat /etc/bandit_pass/bandit33
```

Output:

```text
tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0
```

Success.

---

## Password Obtained

```text
tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0
```

---

## Key Takeaways

Restricted environments often contain escape paths.

Useful trick:

Spawn current shell:

```bash
$0
```

Linux commands are case-sensitive:

```bash
ls
```

is not:

```bash
LS
```
