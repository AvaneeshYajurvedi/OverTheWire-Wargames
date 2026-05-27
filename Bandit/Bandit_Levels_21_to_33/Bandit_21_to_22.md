# Bandit Level 21 → Level 22

##  Level Goal

A program is running automatically at regular intervals using:

```text
cron
```

The challenge hint says:

> Look in `/etc/cron.d/` for the configuration and identify what command is being executed.

The objective is to determine what the scheduled task does and retrieve the next password.

---

##  Step 1: Login

Connect using credentials from the previous level:

```bash
ssh bandit21@bandit.labs.overthewire.org -p 2220
```

Enter password from Level 20:

```text
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

Login successful.

---

##  Step 2: Explore Cron Configuration

Move to cron configuration directory:

```bash
cd /etc/cron.d
```

List files:

```bash
ls -la
```

Output:

```text
behemoth4_cleanup
clean_tmp
cronjob_bandit22
cronjob_bandit23
cronjob_bandit24
...
```

Interesting.

The Bandit challenge likely corresponds to:

```text
cronjob_bandit22
```

---

##  Step 3: Inspect the Cron Job

Read its contents:

```bash
cat cronjob_bandit22
```

Output:

```text
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

Explanation:

```text
* * * * *
```

Means:

```text
Every minute
```

A script executes automatically as:

```text
bandit22
```

The script location:

```text
/usr/bin/cronjob_bandit22.sh
```

---

## 🛠 Step 4: Inspect the Script

Read it:

```bash
cat /usr/bin/cronjob_bandit22.sh
```

Output:

```bash
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

Understanding the script:

First:

```bash
chmod 644
```

Makes the file readable.

Then:

```bash
cat /etc/bandit_pass/bandit22
```

Copies Bandit22 password into:

```text
/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

Interesting.

The cron job itself exposes the password.

---

##  Step 5: Read the Generated File

Open it:

```bash
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

Output:

```text
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```

Success.

---

##  Final Answer

Password for **Bandit Level 22**:

```text
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```

---

##  Key Takeaways

- Cron automates recurring tasks.
- Cron jobs can expose sensitive information.
- Always inspect scheduled tasks during enumeration.
- Understanding system automation reveals attack surfaces.

Useful locations:

```text
/etc/cron.d/
/etc/crontab
/var/spool/cron/
```

Useful commands:

```bash
cat
ls -la
chmod
```

---

