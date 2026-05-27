# Bandit Level 11 → Level 12

##  Level Goal

The password for the next level is stored in `data.txt`.

The contents are encrypted using a Caesar Cipher (ROT13), and we need to decrypt it.

---

##  Step 1: Connect via SSH

Log in using credentials obtained from the previous level:

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

After entering the password from Level 10, access is granted.

---

##  Step 2: Check Available Files

```bash
ls
```

### Output

```text
data.txt
```

Read the file:

```bash
cat data.txt
```

### Output

```text
Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
```

---

##  Step 3: Identify the Encryption

Looking carefully:

```text
Gur cnffjbeq vf
```

The structure resembles readable English after character shifting.

This strongly suggests a **Caesar Cipher**.

A Caesar Cipher shifts letters by a fixed number.

Since the shift value was not provided, instead of manually testing every possibility, I used my own Python brute-force script.

---

##  Step 4: Brute Force Every Shift Value

Python script used:

```python
def brute_force(ciphertext):
    for shift in range(1,26):
        result=''

        for char in message:

            if 'A'<=char<='Z':
                result += chr(
                    (ord(char)-ord('A')-shift)%26
                    + ord('A')
                )

            elif 'a'<=char<='z':
                result += chr(
                    (ord(char)-ord('a')-shift)%26
                    + ord('a')
                )

            else:
                result += char

        print(f"Shift {shift}: {result}")

message=input("ENTER THE ENCRYPTED TEXT\n")
brute_force(message)
```

---

##  Step 5: Identify the Correct Shift

Output:

```text
Shift 13:
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

Shift value:

```text
13
```

This confirms the cipher is **ROT13**, a Caesar Cipher with a shift of 13.

---

##  Final Answer

The password for **Bandit Level 12** is:

```text
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

---

##  Key Takeaways

- Caesar Cipher shifts letters by a fixed value.
- ROT13 is a Caesar Cipher using a shift of 13.
- Brute forcing all possible shifts is a practical method when the shift value is unknown.
- Building small scripts saves time and develops problem-solving skills.

---

