# Natas0 → Natas1

**URL:** `http://natas0.natas.labs.overthewire.org`  
**Credentials:** `natas0 : <natas0>`  
**Difficulty:** Easy  
**Category:**  Source Code Review 

---

## Objective
To Find The Password To The Next Level


---

## Recon & Observations
- Noticed That The Entire Webpage Just Had The Following Text "You can find the password for the next level on this page."

---

## Vulnerability

-The Page Source Code Had The Password Hardcoded In It

---


## Password Found

<details>
<summary> Reveal Password (Spoiler)</summary>
  natas1 : 0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq
</details>

---
## Key Takeaways
- Developers sometimes hardcode sensitive data (passwords, API keys, tokens)
  directly in HTML — always check page source before anything else
- `Ctrl+U` / `view-source:` is the first recon step on any web target
- Even "invisible" content on a webpage is accessible in the DOM
