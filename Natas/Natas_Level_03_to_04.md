# Natas3 → Natas4

**URL:** `http://natas3.natas.labs.overthewire.org`   
**Difficulty:** Easy  
**Category:** Information Disclosure / robots.txt Enumeration

---

## Objective
Find the password for Natas4 hidden somewhere on the server.

---

## Recon & Observations
- Webpage displayed "There is nothing on this page"
- Checked page source — found an HTML comment:
  `<!-- No more information leaks!! Not even Google will find it this time... -->`
- "Not even Google" hinted at search engine crawling — pointed directly to `robots.txt`

---

## Vulnerability

**Type:** Sensitive Directory Disclosure via `robots.txt`  
**Root Cause:** `robots.txt` is a public file intended to tell search engine crawlers
which paths to avoid indexing. Developers often list sensitive or hidden directories
here — which ironically makes those paths discoverable by anyone who checks the file.
The directory `/s3cr3t/` also had directory listing enabled, exposing `users.txt`.

---

## Exploit

1. Viewed page source and spotted the comment hinting at search engine indexing
2. Navigated to `robots.txt` to check for disallowed paths:

**URL accessed:**
```
http://natas3.natas.labs.overthewire.org/robots.txt
```

**Output:**

User-agent: *

Disallow: /s3cr3t/

3. Navigated directly to the disallowed path:
```
http://natas3.natas.labs.overthewire.org/s3cr3t/
```

4.  Directory listing was enabled — `users.txt` was visible
5. Opened `users.txt` and retrieved the natas4 password

---

## Password Found

<details>
<summary> Reveal Password (Spoiler)</summary>
QryZXc2e0zahULdHrtHxzyYkj59kUxLQ
</details>

---

## Key Takeaways
- `robots.txt` is one of the first files to check on any web target — it is
  designed to hide paths from Google, but is itself fully public and readable
  by anyone, making it a self-documenting list of sensitive directories
- HTML comments in source code are never truly hidden — developers leaving
  hints or debug notes in comments is a common real-world finding
- This is a classic example of **security through obscurity** failing —
  renaming a directory to `/s3cr3t/` provides zero protection if the path
  is disclosed elsewhere
- In real bug bounty recon, always check `robots.txt` before running any
  directory brute-force — it saves time and often reveals exactly what you need
