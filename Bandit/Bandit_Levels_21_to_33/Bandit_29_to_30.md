# OverTheWire Bandit Level 29 → Level 30

## Objective

A Git repository is available for Bandit29.

The objective is to inspect the repository and retrieve the password for Bandit30.

---

## Step 1: Create Working Directory

Create a dedicated folder:

```bash
mkdir ~/bandit29
cd ~/bandit29
```

---

## Step 2: Clone Repository

Clone the remote repository:

```bash
git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo
```

Authentication prompt:

```text
bandit29-git@bandit.labs.overthewire.org's password:
```

Enter password from previous level.

Repository cloned successfully.

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
README.md
```

Read it:

```bash
cat README.md
```

Output:

```text
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```

Interesting.

Password hidden.

---

## Step 4: Check Commit History

View Git history:

```bash
git log
```

Output:

```text
commit ccda64bae05a06bd418b662bfe9b72ef3d839d78

fix username

commit d12b10ac12b5e1a2482190bd384d5f6943b83578

initial commit of README.md
```

No password leaks visible.

Need another approach.

---

## Step 5: Enumerate Branches

Check all available branches:

```bash
git branch -a
```

Output:

```text
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
```

Interesting.

Additional branches exist:

```text
dev
sploits-dev
```

Development branches often contain forgotten information.

---

## Step 6: Switch Branch

Checkout development branch:

```bash
git checkout dev
```

Output:

```text
branch 'dev' set up to track 'origin/dev'
Switched to a new branch 'dev'
```

Check files:

```bash
ls
```

Output:

```text
code
README.md
```

Open README again:

```bash
cat README.md
```

Output:

```text
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
```

Success.

Password found.

---

## Password Obtained

```text
qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
```

Bandit29 completed successfully.

---

## Key Takeaways

Git investigations are not limited to:

```bash
git log
```

Always enumerate:

```bash
git branch -a
```

Developers sometimes expose sensitive information inside:

- Development branches
- Feature branches
- Experimental branches

Useful commands:

List branches:

```bash
git branch -a
```

Switch branch:

```bash
git checkout BRANCH_NAME
```


