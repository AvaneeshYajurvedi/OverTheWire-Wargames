# Bandit Level 10 → Level 11

##  Level Goal

The password for the next level is stored in `data.txt`, which contains **Base64 encoded data**.

The task is to decode the contents and retrieve the password.

---

##  Step 1: Connect via SSH

Log in using credentials obtained from the previous level:

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

After entering the password from Level 9, access to the server is granted.

---

##  Step 2: Read the File

Check the contents of `data.txt`:

```bash
cat data.txt
```

### Output

```text
VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
```

---

##  Step 3: Identify the Encoding

The text appears to be encoded in **Base64**.

Base64 is an encoding method used to represent binary data using printable ASCII characters.

---

##  Step 4: Decode the Data

Decode the Base64 content:

```bash
cat data.txt | base64 -d
```

Or:

```bash
base64 -d data.txt
```

### Output

```text
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

---

##  Final Answer

The password for **Bandit Level 11** is:

```text
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

---

##  Key Takeaways

- Base64 is encoding, not encryption.
- The `base64 -d` command decodes Base64 data.
- Always identify file content before attempting random commands.

---

