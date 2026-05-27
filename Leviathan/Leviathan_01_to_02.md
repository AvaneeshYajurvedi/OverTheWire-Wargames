# Leviathan Level 1 → Level 2

---

##  Level Information

| Category | Details |
|----------|----------|
| Platform | OverTheWire |
| Wargame | Leviathan |
| Level | 1 → 2 |
| Difficulty | Easy |
| Skills Learned | SUID Binaries, `strings`, `ltrace`, Password Analysis |

---

#  Objective

The goal of this level is to obtain the password for `leviathan2`.

---

#  Connection

Connect to the remote machine using SSH.

```bash
ssh leviathan1@leviathan.labs.overthewire.org -p 2223
```

After entering the password for `leviathan1`, we successfully log in. :contentReference[oaicite:0]{index=0}

---

#  Enumeration

List the files in the home directory.

```bash
ls -la
```

## Output

```bash
total 36
drwxr-xr-x   2 root       root        4096 Apr  3 15:19 .
drwxr-xr-x 150 root       root        4096 Apr  3 15:20 ..
-rw-r--r--   1 root       root         220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root       root        3851 Apr  3 15:10 .bashrc
-r-sr-x---   1 leviathan2 leviathan1 15088 Apr  3 15:19 check
-rw-r--r--   1 root       root         807 Mar 31  2024 .profile
```

A binary named `check` stands out immediately.

Notice the permissions:

```bash
-r-sr-x---
```

The `s` bit means the binary runs with the privileges of another user (`leviathan2`).

---

#  Inspecting the Binary

Check the binary type.

```bash
file check
```

## Output

```bash
check: setuid ELF 32-bit LSB executable
```

This confirms it is a SUID executable.

---

#  Extracting Readable Strings

Use `strings` to inspect readable content inside the binary.

```bash
strings check
```

Interesting output:

```bash
password:
Wrong password, Good Bye ...
/bin/sh
secr
love
```

The words `secr` and `love` appear suspicious.

---

#  Running the Program

Execute the binary.

```bash
./check
```

It prompts for a password.

```bash
password:
```

Entering random text results in failure.

```bash
Wrong password, Good Bye ...
```

---

#  Dynamic Analysis with ltrace

Use `ltrace` to monitor library calls made by the program.

```bash
ltrace ./check
```

Enter a sample password like:

```txt
test
```

## Output

```bash
strcmp("tes", "sex") = 1
```

This is the key discovery.

The program compares the first three characters of our input against:

```txt
sex
```

---

#  Exploitation

Run the binary again.

```bash
./check
```

Enter the discovered password:

```txt
sex
```

Successful shell spawn:

```bash
$ whoami
leviathan2
```

We now have a shell as `leviathan2`.

---

#  Retrieving the Password

Read the password file.

```bash
cat /etc/leviathan_pass/leviathan2
```

## Output

```txt
NsN1HwFoyN
```

---

#  Password

```txt
NsN1HwFoyN
```

---

#  Commands Used

```bash
ls -la
file check
strings check
./check
ltrace ./check
cat /etc/leviathan_pass/leviathan2
```

---

#  Key Takeaways

- SUID binaries execute with the permissions of their owner
- `strings` helps reveal hidden information inside binaries
- `ltrace` is extremely useful for tracing function calls like `strcmp`
- Dynamic analysis is often faster than reverse engineering
- Many beginner privilege escalation challenges rely on weak string comparisons

---

#  Full Exploitation Flow

```bash
ssh leviathan1@leviathan.labs.overthewire.org -p 2223

ls -la

file check

strings check

ltrace ./check

./check

password: sex

whoami

cat /etc/leviathan_pass/leviathan2
```

---

# Conclusion

This level introduced basic binary analysis using Linux tools like `strings` and `ltrace`.

By tracing the `strcmp()` call, we discovered the hardcoded password used by the program. Since the binary was running with SUID permissions, successful authentication granted us a shell as `leviathan2`, allowing access to the next password.

Some doors are locked with steel.  
Others are locked with terrible coding practices.

---

