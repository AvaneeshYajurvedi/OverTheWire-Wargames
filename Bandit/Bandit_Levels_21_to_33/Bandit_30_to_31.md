# OverTheWire Bandit Level 30 → Level 31

## Objective

A Git repository is provided.

The goal is to inspect the repository and retrieve the password for Bandit31.

---

## Step 1: Create Working Directory

Create a folder:

```bash
mkdir ~/bandit30
cd ~/bandit30
```

---

## Step 2: Clone Repository

Clone the remote repository:

```bash
git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo
```

Authentication prompt:

```text
bandit30-git@bandit.labs.overthewire.org's password:
```

Enter Bandit30 password.

Repository cloned successfully.

---

## Step 3: Inspect Repository Contents

Move into repository:

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

Read contents:

```bash
cat README.md
```

Output:

```text
just an empty file... muahaha
```

Interesting.

Nothing useful stored directly.

---

## Step 4: Inspect Commit History

Check Git history:

```bash
git log
```

Output:

```text
commit e761c5d8e8d01ea9567e35cafe0d58e0e540397a

initial commit of README.md
```

Only one commit exists.

No leaked credentials.

Need another approach.

---

## Step 5: Enumerate Git Tags

Git stores information beyond:

- commits
- branches

Check tags:

```bash
git tag
```

Output:

```text
secret
```

Interesting.

A hidden object exists.

---

## Step 6: Inspect Tag Contents

Show tag:

```bash
git show secret
```

Output:

```text
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
```

Password found.

---

## Password Obtained

```text
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
```

Bandit30 completed successfully.

---

## Key Takeaways

Git repositories contain more than files.

Always enumerate:

Branches:

```bash
git branch -a
```

Commit history:

```bash
git log
```

Tags:

```bash
git tag
```

Inspect objects:

```bash
git show OBJECT_NAME
```
