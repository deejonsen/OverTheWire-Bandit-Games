---
# OverTheWire Bandit Level 14 Walkthrough

---
## **Previous Level:** Level 13

**Login:**

**SSH:** ` ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220`

**Password:** - (Private Key from Level 14)


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 14 → 15**, focusing on using `netcat` (nc) to submit a password to a local service and retrieve the next level's credentials.

## **Problem Statement**
The password for the next level can be retrieved by submitting the password of the current level to **port 30000 on localhost**.
Localhost is a hostname and its IP address is `‘127.0.0.1’`. It is used to access network services on the same device that is running these services.

`nc` or `netcat` is a command that allows to read and write data over a network connection. It can be used for TCP and UDP connections. To connect to a service (as client) on a network the command syntax is the following: `nc <host> <port>`. To create a server that listens to incoming packets, the command looks like this: `nc -l <port>`.


### **Task**:
- Submit the current level's password to port `30000` on `localhost` to receive the password for `bandit15`.
  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit14` (via SSH key from Level 13)


### **Challenge**:  
- The password must be sent to a local service running on port `30000`. 

---

## 🚀**Solution Approach**
1. **Retrieve Current Password**: Read `/etc/bandit_pass/bandit14`.  
2. **Submit Password via `netcat`**: Use `nc localhost 30000` to send the password to the service.

---


### **Code Example** 

```bash
# Log into bandit14 using the SSH key
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

### Get the Current Password
```bash
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
MU4VWeTyJk8ROof199mcBPaLh7lDCPvS
```

### Submit the password to port 30000
```bash
bandit14@bandit:~$ nc localhost 30000
MU4VWeTyJk8ROof199mcBPaLh7lDCPvS  # Paste/press Enter
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo   # Password for bandit15
```

So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit14.html](https://overthewire.org/wargames/bandit/bandit14.html)

---

## Key Takeaways

- **`netcat` (nc):**
  - A versatile networking tool for interacting with TCP/UDP services.
  - Syntax: `nc <host> <port>` to connect to a service.

- **Localhost:**
- Refers to the local machine (`127.0.0.1`).

- **Service Interaction:**
  - Many CTF challenges involve sending data to a port to trigger a response.
 
  
## References
- [OverTheWire Bandit Level 14](https://overthewire.org/wargames/bandit/bandit14.html)
- [Linux `netcat` Guide](https://linux.die.net/man/1/nc)


 ## Additional Notes
 - **Alternative Tools:**
    - Use `telnet localhost 30000` if `nc` is unavailable.
    - For encrypted communication: `openssl s_client -connect localhost:30000`.

- **Troubleshooting:**
  - No response? Ensure the service is running on the correct port.
  - Use `nmap -p 30000 localhost` to verify port status.

Next Level: [Bandit Level 15 → 16](https://github.com/deejonsen/OverTheWire-Bandit-Games/blob/main/Bandit_Level_15.md)

---


![Screenshot 2025-04-14 183041](https://github.com/user-attachments/assets/25739f9e-2056-4ec4-a1a8-a38984fd3ae2)
![Screenshot 2025-04-14 183109](https://github.com/user-attachments/assets/a1451847-e422-47ee-ab91-f79b3b5eaf6a)
![Screenshot 2025-04-14 183251](https://github.com/user-attachments/assets/f29d1985-a25f-4b43-9a0e-3f54f8f4223c)
