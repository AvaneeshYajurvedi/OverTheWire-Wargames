# Bandit Level 16 → Level 17

##  Level Goal

The password for the next level is obtained by connecting to the correct service running on one of several ports.

The service:

- Runs on localhost
- Uses SSL/TLS
- Exists somewhere between ports:

```text
31000 - 32000
```

The challenge is identifying the correct port and retrieving credentials.

---

##  Step 1: Login

Connect using the password from the previous level:

```bash
ssh bandit16@bandit.labs.overthewire.org -p 2220
```

Enter password:

```text
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

---

##  Step 2: Scan Open Ports

Use Nmap to identify listening services:

```bash
nmap -sV localhost -p 31000-32000
```

Output:

```text
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
```

Observations:

- Several ports provide simple echo services
- Two ports use SSL:
  - 31518
  - 31790

Port **31790** looked promising because Nmap could not identify the service.

---

##  Step 3: Connect Using OpenSSL

Connect:

```bash
openssl s_client -connect localhost:31790
```

SSL handshake succeeds.

Certificate information appears:

```text
CN = SnakeOil
TLSv1.3
Cipher = TLS_AES_256_GCM_SHA384
```

Enter current Bandit16 password:

```text
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

Response:

```text
KEYUPDATE

Wrong! Please enter the correct current password.
```

Something was not working correctly.

---

##  Step 4: Retry Using Quiet Mode

Retry using:

```bash
openssl s_client -connect localhost:31790 -quiet
```

Quiet mode removes extra SSL output and allows cleaner interaction.

Enter password again:

```text
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

Server response:

```text
Correct!
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```

Success.

Instead of giving a password directly, the service provides an SSH private key.

---

##  Step 5: Save SSH Key Locally

Exit Bandit:

```bash
exit
```

Create a file locally:

```bash
vim sshkey1.private
```

Paste private key contents.

Save file.

Set permissions:

```bash
chmod 600 sshkey1.private
```

---

##  Step 6: Login Using SSH Key

Use private key authentication:

```bash
ssh -i sshkey1.private \
bandit17@bandit.labs.overthewire.org \
-p 2220
```

Login successful.

Output:

```text
bandit17@bandit:~$
```

Boom. Done.

---

##  Result

Successfully accessed:

```text
bandit17
```

---

##  Key Takeaways

- Enumeration comes before exploitation.
- `nmap -sV` identifies service types and versions.
- SSL services often require `openssl s_client`.
- `-quiet` can simplify interactive SSL communication.
- SSH private keys must have secure permissions (`chmod 600`).
- Sometimes the answer isn't a password—it is a credential that unlocks the next door.

---

