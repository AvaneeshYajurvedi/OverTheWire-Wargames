# Bandit Level 0 → Level 1

##  Level Goal

Log into the Bandit server using SSH and retrieve the password for the next level.

---

##  Step 1: Connect via SSH

To access the Bandit server, we use SSH with the provided credentials:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

* **Username:** `bandit0`
* **Port:** `2220`
* **Password:** `bandit0`

After entering the password, we successfully log into the remote machine.

---

##  Step 2: List Files in the Home Directory

Once logged in, we check the contents of the current directory:

```bash
ls
```

### Output:

```
readme
```

There is a single file named `readme`.

---

##  Step 3: Read the File

To view the contents of the file, we use:

```bash
cat readme
```

### Output:

```
Congratulations on your first steps into the bandit game!!
...
The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

---

##  Final Answer

The password for **Bandit Level 1** is:

```
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

---

##  Key Takeaways

* Learned how to connect to a remote server using SSH.
* Used basic Linux commands:

  * `ls` to list files
  * `cat` to read file contents
* Understood that important information is often stored in plain files.

---

##  Progress

✔ Successfully completed Level 0
➡ Ready for Level 1

---



