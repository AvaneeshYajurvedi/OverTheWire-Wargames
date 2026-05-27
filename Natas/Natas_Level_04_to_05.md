# Natas4 → Natas5

**URL:** `http://natas4.natas.labs.overthewire.org`   
**Difficulty:** Easy  
**Category:** HTTP Header Manipulation / Referer Spoofing

---

## Objective
Gain access to the page which only grants entry to users visiting
from `http://natas5.natas.labs.overthewire.org/`.

---

## Recon & Observations
- Page displayed: `Access disallowed. You are visiting from "" while authorized
  users should come only from "http://natas5.natas.labs.overthewire.org/"`
- Clicking "Refresh page" updated the message to show the current origin:
  `You are visiting from "http://natas4.natas.labs.overthewire.org/index.php"`
- The server was clearly reading the `Referer` HTTP header to determine
  where the request originated from and granting/denying access based on it

---

## Vulnerability

**Type:** Client-Side Trust / HTTP Referer Header Spoofing  
**Root Cause:** The server uses the `Referer` header to implement access control,
trusting it as a reliable indicator of request origin. Since HTTP headers are
fully client-controlled, any user can set the `Referer` to any arbitrary value
— making this an entirely bypassable authentication mechanism.

---

## Exploit

1. Identified that access control was based solely on the `Referer` header
2. Used `curl` to manually set the `Referer` header to the expected value
   while sending a valid authenticated request

**Command:**
```
curl -u natas4:QryZXc2e0zahULdHrtHxzyYkj59kUxLQ \
     --referer http://natas5.natas.labs.overthewire.org/ \
     http://natas4.natas.labs.overthewire.org
```
---


## Password Found

<details>
<summary> Reveal Password (Spoiler)</summary>
natas5 : 0n35PkggAPm2zbEpOU802c0x0Msn1ToK
</details>

---

## Key Takeaways
- The `Referer` header is fully client-controlled and should **never** be used
  as an access control mechanism — it is trivially spoofed with curl, Burp Suite,
  or any HTTP client that allows custom headers
- This is a textbook case of broken access control (OWASP Top 10 #1) —
  the server trusts client-supplied data to make a security decision
- `curl` flags to remember for web testing:
  - `-u user:pass` → HTTP Basic Auth
  - `--referer <url>` → spoof the Referer header
  - `-H "HeaderName: value"` → set any arbitrary header
- In Burp Suite this same attack takes 2 clicks — intercept the request,
  add `Referer: http://natas5.natas.labs.overthewire.org/` in the headers tab,
  forward it
