# Krypton Level 0 → Level 1

---

##  Level Information

| Category | Details |
|----------|----------|
| Platform | OverTheWire |
| Wargame | Krypton |
| Level | 0 → 1 |
| Difficulty | Very Easy |
| Skills Learned | Base64 Decoding, Basic Cryptography Concepts |

---

#  Objective

The goal of this level is to decode the given Base64 string and use it as the password for the next level.

---

#  Given Ciphertext

```txt
S1JZUFRPTklTR1JFQVQ=
```

The challenge description hints that the string is encoded using Base64.

---

#  Understanding Base64

Base64 is an encoding scheme used to represent binary data in ASCII format.

It is commonly used in:
- Email attachments
- Web tokens
- APIs
- Obfuscated text storage

Base64 is **encoding**, not encryption.  
Anyone can decode it easily without a key.

---

#  Decoding the String

The encoded text was decoded using:

```txt
https://www.base64encode.org/
```

Decoded output:

```txt
KRYPTONISGREAT
```

---

#  Password

```txt
KRYPTONISGREAT
```

---

#  SSH Login

Use the decoded password to connect to the next level.

```bash
ssh krypton1@krypton.labs.overthewire.org -p 2231
```

Password:

```txt
KRYPTONISGREAT
```

Successful login confirms the password is correct.

---

#  Alternative Linux Method

Instead of using an online decoder, the same result could be achieved directly from the terminal.

```bash
echo "S1JZUFRPTklTR1JFQVQ=" | base64 -d
```

## Output

```txt
KRYPTONISGREAT
```

---

#  Key Takeaways

- Base64 is an encoding format, not secure encryption
- Encoded strings often end with:
  - `=`
  - `==`
- Linux provides built-in tools like `base64` for decoding
- Always identify whether data is encoded or encrypted before attacking it

---

#  Full Process

```bash
Given string:
S1JZUFRPTklTR1JFQVQ=

Decoded using Base64:
KRYPTONISGREAT

SSH Login:
ssh krypton1@krypton.labs.overthewire.org -p 2231
```

---

#  Conclusion

This level served as a warm-up introduction to basic cryptography concepts.

---

