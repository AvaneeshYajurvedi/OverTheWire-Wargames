# Leviathan Level 0 → Level 1

---

##  Level Information

| Category | Details |
|----------|----------|
| Platform | OverTheWire |
| Wargame | Leviathan |
| Level | 0 → 1 |
| Difficulty | Easy |
| Skills Learned | Linux Enumeration, Hidden Files, Grep Usage |

---

#  Objective

The goal of this level is to retrieve the password for `leviathan1`.

---

#  Connection

Connect to the remote machine using SSH.

```bash
ssh leviathan0@leviathan.labs.overthewire.org -p 2223
```

After entering the password for `leviathan0`, we successfully log in.

---

#  Enumeration

First, list all files including hidden ones.

```bash
ls -la
```

## Output

```bash
total 24
drwxr-xr-x   3 root       root       4096 Apr  3 15:19 .
drwxr-xr-x 150 root       root       4096 Apr  3 15:20 ..
drwxr-x---   2 leviathan1 leviathan0 4096 Apr  3 15:19 .backup
-rw-r--r--   1 root       root        220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root       root       3851 Apr  3 15:10 .bashrc
-rw-r--r--   1 root       root        807 Mar 31  2024 .profile
```

A hidden directory named `.backup` looks interesting.

---

#  Exploring the Backup Directory

Move into the `.backup` directory.

```bash
cd .backup
```

List its contents.

```bash
ls
```

## Output

```bash
bookmarks.html
```

The file name suggests browser bookmark data.

---

#  Finding the Password

Search the file for occurrences of the word `leviathan`.

```bash
cat bookmarks.html | grep "leviathan"
```

## Output

```bash
<DT><A HREF="http://leviathan.labs.overthewire.org/passwordus.html | This will be fixed later, the password for leviathan1 is 3QJ3TgzHDq" ADD_DATE="1155384634" LAST_CHARSET="ISO-8859-1" ID="rdf:#$2wIU71">password to leviathan1</A>
```

The password is directly exposed inside the bookmarks file.

---

#  Password

```txt
3QJ3TgzHDq
```

---

#  Commands Used

```bash
ls -la
cd .backup
ls
cat bookmarks.html | grep "leviathan"
```

---

#  Key Takeaways

- Use `ls -la` to reveal hidden files and directories
- Backup directories can contain sensitive information
- Browser bookmark files may accidentally leak credentials
- `grep` is useful for quickly filtering relevant information

---

#  Full Session Log

```bash
ssh leviathan0@leviathan.labs.overthewire.org -p 2223

ls -la

cd .backup

ls

cat bookmarks.html | grep "leviathan"
```

---

#  Conclusion

This level focused on simple Linux enumeration and hidden file discovery.

By checking hidden directories and inspecting backup files, we were able to retrieve the password for `leviathan1`.

A tiny forgotten bookmark became the key to the next door.

---

