# Natas8 → Natas9

**URL:** `http://natas8.natas.labs.overthewire.org`   
**Difficulty:** Easy  
**Category:** Source Code Review / Encoding Reversal

---

## Objective
Reverse engineer the encoding function from the source code to recover
the original secret and submit it to retrieve the Natas9 password.

---

## Recon & Observations
- Page had an "Input secret" box and a "View sourcecode" link
- Source code revealed the encoded secret and the exact encoding function:
```
$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}
```

- The encoding pipeline was:
  `secret → base64_encode → strrev → bin2hex`
- To recover the secret, simply reverse each step in opposite order:
  `hex2bin → strrev → base64_decode`

---

## Vulnerability

**Type:** Insecure Encoding / Security Through Obscurity  
**Root Cause:** The "secret" is encoded using a chain of reversible
transformations — base64, string reversal, and hex encoding. None of these
are encryption or hashing — they are purely encoding steps, meaning anyone
with access to the algorithm (exposed here via source code) can trivially
reverse it. Encoding is not the same as encryption.

---

## Exploit

Reversed the encoding pipeline step by step:

**Step 1 — hex2bin** (reverse of `bin2hex`):

3d3d516343746d4d6d6c315669563362  →  ==QcCtmMml1ViV3b

**Step 2 — strrev** (reverse of `strrev`):

==QcCtmMml1ViV3b  →  b3ViV1lmMmtCcQ==

**Step 3 — base64_decode** (reverse of `base64_encode`):

b3ViV1lmMmtCcQ==  →  oubWYf2kBq

**Output:**

oubWYf2kBq

**Step 4 -** Entered `oubWYf2kBq` into the "Input secret" form and submitted

## Password Found

<details>
<summary> Reveal Password (Spoiler)</summary>
ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t 
</details>

---

## Key Takeaways
- **Encoding is not encryption** — base64, hex, and string reversal are all
  fully reversible without any key. Storing or comparing secrets using only
  encoding is equivalent to storing them in plaintext
- When you see a comparison function in source code, always ask:
  "Can I reverse this pipeline?" — if there is no key or salt involved,
  the answer is almost always yes
- Secrets should be stored as salted hashes (bcrypt, argon2, SHA-256 with salt)
  — not encoded values. An attacker with the algorithm can always reverse encoding,
  but cannot reverse a proper cryptographic hash
- The one-liner approach (`xxd | rev | base64 -d`) is a useful pattern —
  build comfort piping encoding/decoding tools together in the terminal,
  it comes up constantly in CTFs and real crypto challenges
- Exposed source code massively reduces attacker effort — in this case it
  handed over the entire algorithm, turning a crypto challenge into a
  mechanical reversal
