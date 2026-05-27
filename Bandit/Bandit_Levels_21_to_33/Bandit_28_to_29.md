# OverTheWire Bandit Level 28 → Level 29

## Objective

A Git repository is available:

```text
ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo
```

The goal is to inspect the repository and retrieve the password for the next level.

---

## Step 1: Create Working Directory

Create a folder locally:

```bash
mkdir ~/bandit28
cd ~/bandit28
```

Verify location:

```bash
ls
```

Directory is empty.

---

## Step 2: Clone Repository

Clone the remote Git repository:

```bash
git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo
```

Authentication prompt appears:

```text
bandit28-git@bandit.labs.overthewire.org's password:
```

Enter Bandit28 password.

Clone successful.

---

## Step 3: Inspect Repository Files

Move inside:

```bash
cd repo
```

List files:

```bash
ls
```

Output:

```text
README.md
```

First attempt:

```bash
cat README
```

Output:

```text
cat: README: No such file or directory
```

Small mistake.

Correct filename:

```bash
cat README.md
```

Output:

```text
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```

Interesting.

Password is hidden.

Need another approach.

---

## Step 4: Inspect Git History

View commit history:

```bash
git log
```

Output:

```text
commit 00daa614aac60bd2981c381484191eb7bc4dcfd9
Author: Morla Porla

fix info leak

commit a1487fd098591dfa210ede70ba60f7093f47d20d

add missing data

commit eaef76e40b22863d8085130677ae53e13ae1a9c6

initial commit
```

Interesting commit:

```text
fix info leak
```

That sounds suspicious.

---

## Step 5: Inspect Previous Changes

View commit contents:

```bash
git show 00daa614aac60bd2981c381484191eb7bc4dcfd9
```

Output:

```diff
- password: 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
+ password: xxxxxxxxxx
```

Found it.

The password existed previously and was hidden later.

Git history still preserved it.

---

## Password Obtained

```text
4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
```

---

## Key Takeaways

Git preserves historical commits.

Removing secrets from current files does not erase them from repository history.

Useful commands:

View commit history:

```bash
git log
```

Inspect commit contents:

```bash
git show COMMIT_HASH
```

