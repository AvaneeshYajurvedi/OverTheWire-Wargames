# Natas10 → Natas11

**URL:** `http://natas10.natas.labs.overthewire.org`   
**Difficulty:** Easy  
**Category:** Command Injection (Filtered)

---

## Objective
Bypass the character filter and exploit the search functionality to read
the Natas11 password from the server filesystem.

---

## Recon & Observations
- Page displayed: "For security reasons, we now filter on certain characters"
- Same input box as Natas9 but with a filter applied
- Checked source code:
```
$key = "";
if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}
if($key != "") {
    if(preg_match('/[;|&]/', $key)) {
        print "Input contains an illegal character!";
    } else {
        passthru("grep -i $key dictionary.txt");
    }
}
```

- The filter blocks `;`, `|`, and `&` — the metacharacters used in Natas9
- However the input is still passed raw into `grep` inside `passthru()`
- `grep` itself can be weaponized without any shell metacharacters — it accepts
  multiple file arguments natively, so we can pass the password file directly
  as a second target and use `#` to comment out `dictionary.txt`

---

## Vulnerability

**Type:** OS Command Injection (Filter Bypass)  
**Root Cause:** The filter only blocks `;`, `|`, and `&` — it does not account
for the fact that `grep` accepts multiple file paths as arguments. By passing
the password file as part of the grep arguments and using `#` to comment out
the rest of the command, injection is still achievable without any of the
blocked characters. The root issue remains the same as Natas9 — unsanitized
user input concatenated into a shell command.

---

## Exploit

1. Confirmed `;`, `|`, and `&` were blocked by the regex filter
2. Recognized that `grep` natively supports multiple file arguments —
   no shell chaining needed
3. Used `.` as the grep pattern (matches any character — returns every line)
   and passed the password file as the search target, then used `#` to
   comment out `dictionary.txt` so it wouldn't interfere

**Payload entered into the input box:**

. /etc/natas_webpass/natas11 #

**Resulting command executed on the server:**
```
grep -i . /etc/natas_webpass/natas11 # dictionary.txt
```

- `.` matches every line in the file
- `/etc/natas_webpass/natas11` is passed as the file for grep to search
- `#` comments out `dictionary.txt` — it is never read
- grep prints the full contents of the password file directly to the page

---

## Password Found

<details>
<summary> Reveal Password (Spoiler)</summary>
UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk
</details>

---

## Key Takeaways
- Blocklists are almost always bypassable — blocking a specific set of
  characters does not eliminate an injection vulnerability, it just raises
  the bar slightly. Allowlists (only permit known-safe characters) are the
  correct mitigation
- `grep` is itself an injection vector — it accepts multiple file paths as
  arguments, so you don't need shell chaining metacharacters to read
  arbitrary files with it
- `#` is a shell comment character — anything after it on the same line is
  ignored by the shell, making it useful for neutralizing trailing arguments
  without needing `;` or `|`
- The `.` regex pattern in grep matches any single character — effectively
  matching every non-empty line in a file, making it a useful wildcard
  when you want to dump entire file contents
- The key lesson: when a filter blocks your payload, don't just try
  different metacharacters — rethink the attack entirely. Here the solution
  was to abuse `grep`'s own argument handling rather than chain shell commands
