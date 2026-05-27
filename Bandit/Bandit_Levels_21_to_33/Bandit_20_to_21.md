# Bandit Level 20 → Level 21

##  Level Goal

There is a binary named:

```text
suconnect
```

The level description explains:

- The program connects to a port on localhost
- It reads a password from that connection
- If the password matches the current Bandit password
- The program sends the password for the next level

The challenge becomes:

> Create a service locally that `suconnect` can connect to.

---

##  Step 1: Login

Connect using credentials from the previous level:

```bash
ssh bandit20@bandit.labs.overthewire.org -p 2220
```

Enter password:

```text
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

Login successful.

---

##  Step 2: Check Available Files

List files:

```bash
ls
```

Output:

```text
suconnect
```

Interesting.

Only one binary exists.

---

##  Step 3: Test the Binary

Try running:

```bash
./suconnect 1234
```

Output:

```text
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
Read: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
Password matches, sending next password
```

Observation:

```text
suconnect expects a connection on a port.
```

No listener exists yet.

That means we must create one ourselves.

---

##  Step 4: Open Second Terminal

Open another terminal.

SSH into Bandit20 again:

```bash
ssh bandit20@bandit.labs.overthewire.org -p 2220
```

Create a Netcat listener:

```bash
nc -lvp 1234
```

Output:

```text
Listening on 0.0.0.0 1234
```

Now Bandit20 is waiting for connections.

---

##  Step 5: Trigger Connection

Go back to the first terminal.

Run:

```bash
./suconnect 1234
```

The binary connects to localhost port:

```text
1234
```

---

##  Step 6: Send Current Password

Second terminal receives:

```text
Connection received on localhost
```

Provide Bandit20 password:

```text
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

Output:

```text
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

Success.

The next password appears.

---

##  Final Answer

Password for **Bandit Level 21**:

```text
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

---

##  Key Takeaways

- `nc -lvp PORT` creates a listening server.
- Some binaries connect outward instead of waiting for input.
- Networking challenges often require multiple terminals.
- Understanding client-server communication is critical.

Commands learned:

Create listener:

```bash
nc -lvp 1234
```

Connect binary:

```bash
./suconnect 1234
```

---

