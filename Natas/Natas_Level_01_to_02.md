# Natas1 → Natas2

**URL:** `http://natas1.natas.labs.overthewire.org`    
**Difficulty:** Easy  
**Category:**  Source Code Review 

---

## Objective
To Find The Password To The Next Level

---

## Recon & Observations
- The webpage said that right click has been blocked and the password to the next level is on the webpage itself

---

## Vulnerability

- The Page Source Code Had The Password Hardcoded In It

---

## Exploit
```
Ctrl + U gave out the page source code
```

---

## Password Found
<details>
<summary> Reveal Password (Spoiler)</summary>
  natas2 : TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI
</details>

---


## Key Takeaways
- Developers sometimes hardcode sensitive data (passwords, API keys, tokens)
  directly in HTML — always check page source before anything else
- `Ctrl+U` / `view-source:` is the first recon step on any web target
- Even "invisible" content on a webpage is accessible in the DOM

---
