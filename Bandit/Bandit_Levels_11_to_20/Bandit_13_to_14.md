# Bandit Level 13 → Level 14

##  Level Goal

The password for the next level is not stored directly.

Instead, Bandit provides an SSH private key that must be used to log into the next account.

---

##  Step 1: Login

Connect using the password from the previous level:

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

---

##  Step 2: Check Available Files

List files:

```bash
ls
```

Output:

```text
HINT
sshkey.private
```

Read the hint:

```bash
cat HINT
```

Important information:

```text
The current version of OverTheWire prevents logging in
from one level to another via localhost.
```

This becomes important later.

---

##  Step 3: Inspect the Private Key

View the key:

```bash
cat sshkey.private
```

Output begins:

```text
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEA...
```

This indicates an SSH private key.

---

##  Step 4: First Attempt (Failed)

Attempt to change permissions:

```bash
chmod 600 sshkey.private
```

Output:

```text
Operation not permitted
```

Checking permissions:

```bash
ls -l sshkey.private
```

Output:

```text
-rw-r----- 1 bandit14 bandit13 1679 sshkey.private
```

Since the home directory is restricted, copy the key:

```bash
cp sshkey.private /tmp/avii_key
chmod 600 /tmp/avii_key
```

Attempt login:

```bash
ssh -i /tmp/avii_key bandit14@localhost -p 2220
```

Output:

```text
Connecting from localhost is blocked
```

OverTheWire intentionally prevents localhost authentication.

---

##  Step 5: Move the Key to Local Machine

From local terminal:

```bash
scp -P 2220 \
bandit13@bandit.labs.overthewire.org:sshkey.private .
```

Enter the Bandit13 password.

Adjust permissions locally:

```bash
chmod 700 sshkey.private
```

---

##  Step 6: Login Using SSH Key

Use the private key directly from your machine:

```bash
ssh -i sshkey.private \
bandit14@bandit.labs.overthewire.org \
-p 2220
```

Login successful.

---

##  Step 7: Retrieve Password

Read password file:

```bash
cat /etc/bandit_pass/bandit14
```

Output:

```text
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

---

##  Final Answer

Password for **Bandit Level 14**:

```text
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

---

##  Key Takeaways

- SSH private keys can authenticate without passwords.
- File permissions matter for SSH keys.
- Read hint files carefully.
- When one path fails, pivot and adapt.
- Troubleshooting is part of cybersecurity.

---
