# Bandit Level 14 → Level 15

##  Level Goal

The password for the next level can be retrieved by submitting the current level password to a service running on:

```text
localhost:30000
```

The service listens locally and returns the next password when given the correct input.

---

##  Step 1: Connect via SSH

Login using the password from the previous level:

```bash
ssh bandit14@bandit.labs.overthewire.org -p 2220
```

---

##  Step 2: Inspect Environment

Check files:

```bash
ls -la
```

Output:

```text
.ssh
.bashrc
.profile
```

Nothing immediately useful.

Move into `.ssh`:

```bash
cd .ssh
ls
```

Output:

```text
authorized_keys
```

No password stored there.

Return:

```bash
cd ..
```

---

##  Step 3: Verify Current Password

Bandit14 password:

```bash
cat /etc/bandit_pass/bandit14
```

Output:

```text
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

The level instructions indicate that this password must be submitted to port `30000`.

---

##  Step 4: Connect Using Netcat

Use `nc` (Netcat) to communicate with the local service:

```bash
nc localhost 30000
```

After connecting, submit Bandit14 password:

```text
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

Server response:

```text
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

---

##  Final Answer

Password for **Bandit Level 15**:

```text
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

---

##  Key Takeaways

- `nc` (Netcat) can connect to TCP services.
- Many cybersecurity challenges involve interacting with running services rather than files.
- Localhost services can expose important information.
- Understanding ports and networking is foundational in security.

---

