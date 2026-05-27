# Bandit Level 15 → Level 16

##  Level Goal

The password for the next level can be retrieved by submitting the current password to a service running on:

```text
localhost:30001
```

Unlike the previous level, this service uses **SSL/TLS encryption**.

---

##  Step 1: Connect via SSH

Login using credentials from the previous level:

```bash
ssh bandit15@bandit.labs.overthewire.org -p 2220
```

---

##  Step 2: Inspect Environment

Check files:

```bash
ls
```

Output:

```text
(no files)
```

Nothing useful is stored locally.

The level instructions indicate that the password must be submitted to a service on port `30001`.

Since the previous level used `nc`, it is tempting to try the same approach.

However, this service requires an encrypted SSL/TLS connection.

---

##  Step 3: Connect Using OpenSSL

Use `openssl s_client`:

```bash
openssl s_client -connect localhost:30001
```

Output begins:

```text
CONNECTED
Certificate chain
CN = SnakeOil
TLSv1.3
Cipher is TLS_AES_256_GCM_SHA384
```

Important observations:

- SSL/TLS handshake succeeds
- Server presents a self-signed certificate
- Secure encrypted connection established

---

##  Step 4: Submit Current Password

After the SSL connection remains open, enter the Bandit15 password:

```text
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

Server response:

```text
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

Connection closes.

---

##  Final Answer

Password for **Bandit Level 16**:

```text
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

---

##  Key Takeaways

- `nc` works for plain TCP communication.
- `openssl s_client` works for encrypted SSL/TLS services.
- Certificates help establish secure communication channels.
- Recognizing protocol requirements matters as much as knowing commands.

---

