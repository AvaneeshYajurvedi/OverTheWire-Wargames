# OverTheWire Bandit Level 31 → Level 32

## Objective

A Git repository is provided.

The task:

- Create a file:

```text
key.txt
```

- File contents:

```text
May I come in?
```

- Commit it
- Push it to the remote repository
- Retrieve the password for the next level

---

## Step 1: Create Working Directory

Create a folder:

```bash
mkdir ~/bandit31
cd ~/bandit31
```

---

## Step 2: Clone Repository

Clone repository:

```bash
git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo
```

Authentication prompt:

```text
bandit31-git@bandit.labs.overthewire.org's password:
```

Enter Bandit31 password.

Repository cloned successfully.

---

## Step 3: Inspect Repository

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

Read instructions:

```bash
cat README.md
```

Output:

```text
This time your task is to push a file to the remote repository.

Details:

File name: key.txt
Content: 'May I come in?'
Branch: master
```

Clear objective.

Need to create file.

---

## Step 4: Create Required File

Create:

```bash
echo "May I come in?" > key.txt
```

Verify:

```bash
cat key.txt
```

Output:

```text
May I come in?
```

Success.

---

## Step 5: Add File

Attempt Git tracking:

```bash
git add -f key.txt
```

Important:

```text
-f
```

forces Git to include the file.

---

## Step 6: Commit Changes

Commit:

```bash
git commit -a
```

Output:

```text
[master c6c00e5] Commit
1 file changed, 1 insertion(+)
create mode 100644 key.txt
```

Commit successful.

---

## Step 7: Push Repository

Push changes:

```bash
git push -u origin master
```

Authentication prompt:

```text
bandit31-git@bandit.labs.overthewire.org's password:
```

Enter current password.

Server validates submission.

Output:

```text
### Attempting to validate files... ####
```

Then:

```text
Well done! Here is the password for the next level:
```

Password displayed:

```text
3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
```

Success.

---

## Password Obtained

```text
3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
```

Bandit31 completed successfully.

---

## Key Takeaways

Git workflows include:

Track files:

```bash
git add
```

Commit:

```bash
git commit
```

Push:

```bash
git push
```
