# OverTheWire Bandit Level 27 → Level 28

## Objective

A Git repository is available:

```text
ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo
```

The goal is to clone the repository and find the password for the next level.

---

## Step 1: Create Working Directory

Create a folder locally:

```bash
mkdir ~/bandit27
cd ~/bandit27
```

This keeps repository files organized.

---

## Step 2: Clone Remote Repository

Run:

```bash
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```

Output:

```text
Cloning into 'repo'...
Receiving objects: 100%
```

Authentication required:

```text
bandit27-git@bandit.labs.overthewire.org's password:
```

Enter Bandit27 password:

```text
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

Clone successful.

---

## Step 3: Inspect Repository

List contents:

```bash
ls
```

Output:

```text
repo
```

Move inside:

```bash
cd repo
```

Check files:

```bash
ls
```

Output:

```text
README
```

Interesting.

Only one file exists.

---

## Step 4: Read README

Open file:

```bash
cat README
```

Output:

```text
The password to the next level is:

Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```

Success.

---

## Password Obtained

```text
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```

---

## Key Takeaways

Git repositories can contain sensitive information.

Useful commands:

Clone repository:

```bash
git clone REPOSITORY_URL
```

List files:

```bash
ls
```

Read file:

```bash
cat filename
```


