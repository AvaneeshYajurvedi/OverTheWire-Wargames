# Natas7 → Natas8

**URL:** `http://natas7.natas.labs.overthewire.org`    
**Difficulty:** Easy  
**Category:** Local File Inclusion (LFI)

---

## Objective
Find the password for Natas8 stored somewhere on the server's filesystem.

---

## Recon & Observations
- Page had two navigation links — "Home" and "About"
- Clicking them changed the URL to:
  - `index.php?page=home`
  - `index.php?page=about`
- The `page=` parameter was clearly being used to load content dynamically —
  a textbook LFI indicator
- Checked page source — found an HTML comment:
  `<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 -->`
- Combined the LFI vector with the hinted file path

---

## Vulnerability

**Type:** Local File Inclusion (LFI)  
**Root Cause:** The `page` GET parameter is passed directly into a PHP file
inclusion function (e.g. `include($_GET['page'])`) without any sanitization,
validation, or path restriction. This allows an attacker to supply an arbitrary
filesystem path and have the server read and return any file the web process
has permission to access.

---

## Exploit

1. Noticed the `?page=` parameter loading different content dynamically
2. Found the hint in page source pointing to `/etc/natas_webpass/natas8`
3. Replaced the `page` value with the absolute path to the password file:

**URL accessed:**
```
http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8
```
## Password Found

<details>
<summary> Reveal Password (Spoiler)</summary>
xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q
</details>

---

Key Takeaways

- Any ?page=, ?file=, ?path=, ?template= parameter is an immediate
LFI candidate — if the app loads content based on user-supplied input, test
it with filesystem paths like /etc/passwd first to confirm inclusion
- LFI is one of the most impactful web vulnerabilities — depending on server
config it can expose credentials, SSH keys, source code, and logs, or
escalate to RCE via log poisoning
- HTML comments are always worth reading — developers leave file paths,
credentials, and debug hints in comments more often than you'd expect
- In real bug bounty, a confirmed LFI is typically rated High severity and
can chain into Critical if RCE is achievable via log poisoning or PHP wrappers
