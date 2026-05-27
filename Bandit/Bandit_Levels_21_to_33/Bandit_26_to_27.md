# OverTheWire Bandit Level 26 → Level 27

## Objective

Bandit26 provides access to a special binary:

```text
bandit27-do
```

The goal is to understand how it works and use it to retrieve the Bandit27 password.

---

## Step 1: Continue Using Existing Bandit26 Shell

From the previous level, shell access had already been obtained through Vim escape.

Current shell:

```bash
bandit26@bandit:~$
```

List files:

```bash
ls
```

Output:

```text
bandit27-do
text.txt
```

Interesting.

A binary exists:

```text
bandit27-do
```

Very similar to earlier Bandit privilege execution challenges.

---

## Step 2: Inspect Available Files

Attempt:

```bash
cat text.ttxt
```

Output:

```text
cat: text.ttxt: No such file or directory
```

Typo.

Correct command:

```bash
cat text.txt
```

Output:

```text
  _                     _ _ _   ___   __
 | |                   | (_) | |__ \ / /
 | |__   __ _ _ __   __| |_| |_   ) / /_
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/
```

No password stored there.

Need to investigate the binary.

---

## Step 3: Check Binary Permissions

Run:

```bash
./bandit27-do id
```

Output:

```text
uid=11026(bandit26)
gid=11026(bandit26)
euid=11027(bandit27)
groups=11026(bandit26)
```

Important observation:

```text
euid=11027(bandit27)
```

The binary executes commands with:

```text
bandit27
```

permissions.

This means we can access files Bandit26 normally cannot.

---

## Step 4: Read Bandit27 Password

Run:

```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```

Output:

```text
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

Success.

The binary executed:

```bash
cat /etc/bandit_pass/bandit27
```

with Bandit27 privileges.

---

## Password Obtained

```text
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

---

## Key Takeaways

Privilege execution binaries can run commands using another user's permissions.

Useful command:

Check execution identity:

```bash
id
```

Privilege helper usage:

```bash
./binary command
```

Understanding:

```text
uid  → actual user
euid → effective permissions
```

