# Natas2 → Natas3

**URL:** `http://natas2.natas.labs.overthewire.org`   
**Difficulty:** Easy  
**Category:** Directory Listing / Information Disclosure

---

## Objective
Find the password for Natas3 hidden somewhere on the server.

---

## Recon & Observations
- The webpage just displayed "There is nothing on this page"
- Checked page source — found an `<img>` tag referencing `/files/pixel.png`
- The `/files/` path in the image src suggested a server directory exists beyond what's linked on the page

---

## Vulnerability

**Type:** Directory Listing / Forced Browsing  
**Root Cause:** The web server has directory listing enabled on `/files/`, meaning anyone who knows (or guesses) the path can browse its contents — no authentication required. Sensitive files stored in unprotected directories are fully exposed.

---

## Exploit

1. Viewed page source (`Ctrl+U`) and spotted `/files/pixel.png` in an `<img>` tag
2. Navigated to `http://natas2.natas.labs.overthewire.org/files/` directly in the browser
3. Server returned a directory listing — `users.txt` was visible
4. Opened `users.txt` and found the natas3 credentials

---

**URL accessed:**
```
http://natas2.natas.labs.overthewire.org/files/users.txt
```
---

## Password Found

<details>
<summary> Reveal Password (Spoiler)</summary>
3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH
</details>

---

## Key Takeaways
- Directory listing being enabled on a web server is a misconfiguration that
  exposes the entire folder structure — a real-world finding reportable as a
  vulnerability on bug bounty programs (typically rated Low–Medium)
- Image sources, script srcs, and href attributes in HTML are goldmines during
  recon — they reveal backend paths the UI doesn't visibly link to
- Forced browsing (manually navigating to guessed/discovered paths) is a core
  web recon technique — tools like Gobuster automate this at scale
- Never assume a file is "hidden" just because it isn't linked on the page
