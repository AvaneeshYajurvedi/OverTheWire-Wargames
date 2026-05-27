# Natas6 → Natas7

**URL:** `http://natas6.natas.labs.overthewire.org`  
**Difficulty:** Easy  
**Category:** Source Code Review / Sensitive File Exposure

---

## Objective
Find the secret value and submit it through the input form to retrieve
the password for Natas7.

---

## Recon & Observations
- Page had a single input box labeled "Input secret" with a submit button
- Checked page source — found embedded PHP:
```php
include "includes/secret.inc";
if(array_key_exists("submit", $_POST)) {
    if($secret == $_POST['secret']) {
        print "Access granted. The password for natas7 is ";
    } else {
        print "Wrong secret";
    }
}
```
- The PHP code revealed the secret was being loaded from `includes/secret.inc`
- That file path is directly accessible via the browser since there is no
  access restriction on the `/includes/` directory

---

## Vulnerability

**Type:** Sensitive File Exposure / Source Code Disclosure  
**Root Cause:** The secret is stored in a `.inc` file served from a publicly
accessible directory. While `.inc` files are meant to be included server-side
by PHP, the web server has no rule preventing direct browser access to them —
returning the raw file contents instead of executing them as PHP. Storing
secrets in files within the web root is inherently risky for this reason.

---

## Exploit

1. Read the PHP source and identified the include path: `includes/secret.inc`
2. Navigated directly to the file in the browser:

**URL accessed:**
```
http://natas6.natas.labs.overthewire.org/includes/secret.inc
```
**Output:**

$secret = "FOEIUWGHFEEUHOFUOIU";


3. Entered `FOEIUWGHFEEUHOFUOIU` into the "Input secret" form and clicked Submit

## Password Found

<details>
<summary> Reveal Password (Spoiler)</summary>
  bmg8SvU1LizuWjx3y7xkNERkHxGre0GS
</details>


## Key Takeaways
- `.inc`, `.bak`, `.old`, and `.config` files stored inside the web root are
  a classic misconfiguration — they are intended for internal use but are
  often directly accessible if the server has no deny rules for those extensions
- Always check `include` / `require` paths in PHP source — they reveal server
  file structure and are frequently accessible directly via the browser
- Secrets (API keys, passwords, tokens) should never live inside the web root
  at all — they belong in environment variables or config files outside the
  publicly served directory
- In real-world bug bounty this is a valid finding — exposed `.env` files,
  `config.php.bak`, or `secrets.inc` files have led to critical disclosures
  on major platforms
- This is also why `.htaccess` rules like `Deny from all` on sensitive
  directories matter — without them, any file in the web root is fair game
