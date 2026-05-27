# Bandit Level 22 → Level 23

##  Level Goal

A cron job runs automatically as another user.

The objective:

- Find the cron job
- Understand what it does
- Determine where it stores the password
- Retrieve the password for the next level

---

##  Step 1: Login

Connect using Bandit22 credentials:

```bash
ssh bandit22@bandit.labs.overthewire.org -p 2220
```

Login successful.

---

##  Step 2: Locate Cron Jobs

First attempt:

```bash
cd /etc/cron.df/
```

Output:

```text
-bash: cd: /etc/cron.df/: No such file or directory
```

Mistyped directory name.

Correct path:

```bash
cd /etc/cron.d/
```

Check contents:

```bash
ls -la
```

Output:

```text
cronjob_bandit22
cronjob_bandit23
cronjob_bandit24
```

Since we need Bandit23 password:

```text
cronjob_bandit23
```

looks interesting.

---

##  Step 3: Inspect Cron Configuration

Read cron configuration:

```bash
cat cronjob_bandit23
```

Output:

```text
@reboot bandit23 /usr/bin/cronjob_bandit23.sh &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh &> /dev/null
```

Observation:

The script runs:

```text
every minute
```

as:

```text
bandit23
```

---

##  Step 4: Inspect Script Logic

Open script:

```bash
cat /usr/bin/cronjob_bandit23.sh
```

Output:

```bash
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

Breakdown:

Current user:

```bash
myname=$(whoami)
```

Cron runs script as:

```text
bandit23
```

So:

```text
myname = bandit23
```

Next:

```bash
echo I am user bandit23 | md5sum
```

creates a hashed filename.

---

##  Step 5: Generate Target Filename

Run:

```bash
echo I am user bandit23 | md5sum | cut -d ' ' -f 1
```

Output:

```text
8ca319486bfbbc3663ea0fbe81326349
```

Password file location becomes:

```text
/tmp/8ca319486bfbbc3663ea0fbe81326349
```

---

##  Step 6: Read Password File

Run:

```bash
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```

Output:

```text
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```

Success.

---

##  Final Answer

Password for **Bandit Level 23**:

```text
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```

---

##  Key Takeaways

- Cron jobs automate recurring tasks.
- Read scripts carefully before guessing.
- Hashes are sometimes used as predictable file names.
- Small mistakes are normal — debugging is part of solving.

Useful commands:

Generate MD5:

```bash
echo text | md5sum
```

Extract first field:

```bash
cut -d ' ' -f 1
```

---
