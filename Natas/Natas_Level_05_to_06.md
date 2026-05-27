# Natas5 → Natas6

**URL:** `http://natas5.natas.labs.overthewire.org`    
**Difficulty:** Easy  
**Category:** Cookie Manipulation

---

## Objective
Gain access to the page which requires you to be "logged in".

---

## Recon & Observations
- Page displayed: `Access disallowed. You are not logged in`
- Checked page source — nothing useful
- Opened browser DevTools → Application tab → Cookies
- Found a cookie: `loggedin=0`
- The value `0` clearly mapped to `false` — the server was using this cookie
  to determine authentication state

---

## Vulnerability

**Type:** Client-Side Authentication / Cookie Manipulation  
**Root Cause:** The server trusts a client-controlled cookie (`loggedin=0/1`)
to make authentication decisions without any server-side verification or
signing. Since cookies are stored on the client and freely editable, any user
can modify this value to impersonate an authenticated session.

---

## Exploit

1. Opened DevTools (`F12`) → Application → Cookies →
   `http://natas5.natas.labs.overthewire.org`
2. Located the `loggedin` cookie with value `0`
3. Double-clicked the value and changed it to `1`
4. Refreshed the page

**Cookie before:**

loggedin=0

**Cookie after:**

loggedin=1

**Result:**

Access granted.

## Password Found

<details>
<summary> Reveal Password (Spoiler)</summary>
0RoJwHdSKWFTYR5WuiAewauSuNaBXned
</details>

## Key Takeaways
- Cookies are stored client-side and are fully editable — any authentication
  or authorization logic that relies solely on a cookie value without server-side
  validation or cryptographic signing is trivially bypassable
- This is the same class of vulnerability as the Referer spoof in Natas4 —
  the server is trusting client-controlled data to make a security decision
- In real applications, session state should be managed server-side — the cookie
  should only contain an opaque session ID that maps to server-stored state,
  not a readable flag like `loggedin=1`
- Browser DevTools (Application → Cookies) is the fastest way to inspect and
  modify cookies without any extra tooling — no Burp Suite needed for simple cases
