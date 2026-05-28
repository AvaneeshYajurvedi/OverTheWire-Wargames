# Krypton Level 1 → Level 2

---

##  Level Information

| Category | Details |
|----------|----------|
| Platform | OverTheWire |
| Wargame | Krypton |
| Level | 1 → 2 |
| Difficulty | Easy |
| Skills Learned | Caesar Cipher, ROT13, Brute Force Cryptanalysis, Python Scripting |

---

#  Objective

The goal of this level is to decrypt the contents of the `krypton2` file and retrieve the password for the next level.

---

#  SSH Login

Login using the credentials obtained from the previous level.

```bash
ssh krypton1@krypton.labs.overthewire.org -p 2231
```

After successful authentication, enumerate the available files.

---

#  Enumeration

List the contents of the current directory.

```bash
ls -la
```

Move into the Krypton game directory.

```bash
cd /krypton
ls
```

## Output

```bash
krypton1  krypton2  krypton3  krypton4  krypton5  krypton6  krypton7
```

Navigate into the `krypton1` directory.

```bash
cd krypton1
ls
```

## Output

```bash
krypton2  README
```

Read the challenge description.

```bash
cat README
```

The README mentions:

```txt
The password for level 2 is in the file 'krypton2'.
It is encrypted using a simple rotation called ROT13.
```

---

#  Reading the Ciphertext

Display the contents of the encrypted file.

```bash
cat krypton2
```

## Output

```txt
YRIRY GJB CNFFJBEQ EBGGRA
```

---

#  Identifying the Cipher

The challenge hints toward a rotational cipher.

A rotation cipher is commonly known as a:

- Caesar Cipher
- Shift Cipher

Each letter is shifted by a fixed number of positions in the alphabet.

Since the exact shift value was unknown initially, brute force analysis was used.

---

#  Python Brute Force Script

A custom Python script was written to test all possible Caesar Cipher shifts from `1 → 25`.

```python
def brute_force(ciphertext):
    for shift in range(1, 26):
        result = ''

        for char in message:
            if 'A' <= char <= 'Z':
                result += chr((ord(char) - ord('A') - shift) % 26 + ord('A'))

            elif 'a' <= char <= 'z':
                result += chr((ord(char) - ord('a') - shift) % 26 + ord('a'))

            else:
                result += char

        print(f"Shift {shift}: {result}")

message = input("ENTER THE ENCRYPTED TEXT \n")
brute_force(message)
```

---

#  Script Execution

Input:

```txt
YRIRY GJB CNFFJBEQ EBGGRA
```

Output:

```txt
Shift 1:XQHQX FIA BMEEIADP DAFFQZ
Shift 2:WPGPW EHZ ALDDHZCO CZEEPY
Shift 3:VOFOV DGY ZKCCGYBN BYDDOX
Shift 4:UNENU CFX YJBBFXAM AXCCNW
Shift 5:TMDMT BEW XIAAEWZL ZWBBMV
Shift 6:SLCLS ADV WHZZDVYK YVAALU
Shift 7:RKBKR ZCU VGYYCUXJ XUZZKT
Shift 8:QJAJQ YBT UFXXBTWI WTYYJS
Shift 9:PIZIP XAS TEWWASVH VSXXIR
Shift 10:OHYHO WZR SDVVZRUG URWWHQ
Shift 11:NGXGN VYQ RCUUYQTF TQVVGP
Shift 12:MFWFM UXP QBTTXPSE SPUUFO
Shift 13:LEVEL TWO PASSWORD ROTTEN
Shift 14:KDUDK SVN OZRRVNQC QNSSDM
Shift 15:JCTCJ RUM NYQQUMPB PMRRCL
Shift 16:IBSBI QTL MXPPTLOA OLQQBK
Shift 17:HARAH PSK LWOOSKNZ NKPPAJ
Shift 18:GZQZG ORJ KVNNRJMY MJOOZI
Shift 19:FYPYF NQI JUMMQILX LINNYH
Shift 20:EXOXE MPH ITLLPHKW KHMMXG
Shift 21:DWNWD LOG HSKKOGJV JGLLWF
Shift 22:CVMVC KNF GRJJNFIU IFKKVE
Shift 23:BULUB JME FQIIMEHT HEJJUD
Shift 24:ATKTA ILD EPHHLDGS GDIITC
Shift 25:ZSJSZ HKC DOGGKCFR FCHHSB
```

---

#  Correct Decryption

The meaningful plaintext appears at:

```txt
Shift 13: LEVEL TWO PASSWORD ROTTEN
```

This confirms the cipher used is:

```txt
ROT13
```

ROT13 shifts every alphabet character by 13 positions.

---

#  Password

```txt
ROTTEN
```

---

#  Alternative Linux Method

ROT13 can also be solved directly in Linux using `tr`.

```bash
echo "YRIRY GJB CNFFJBEQ EBGGRA" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

## Output

```txt
LEVEL TWO PASSWORD ROTTEN
```

---

#  Key Takeaways

- ROT13 is a Caesar Cipher with a shift value of 13
- Caesar Ciphers are vulnerable to brute force attacks
- Cryptanalysis often involves testing all possible shifts
- Python is extremely useful for automating cipher analysis
- Recognizable English text helps identify the correct shift quickly

---

#  Commands Used

```bash
ssh krypton1@krypton.labs.overthewire.org -p 2231

cd /krypton

cd krypton1

cat README

cat krypton2
```

---

#  Conclusion

This level introduced classical substitution ciphers through ROT13 encryption.

By recognizing the ciphertext as a Caesar-style rotation cipher and brute forcing all possible shifts with a custom Python script, the hidden password was successfully recovered.

---


