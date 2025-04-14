---
# OverTheWire Bandit Level 15 Walkthrough

---
## **Previous Level:** Level 14

**Login:**

**SSH:** ` ssh bandit15@bandit.labs.overthewire.org -p 2220`

**Password:** `8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo`


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 15 → 16**, focusing on using SSL/TLS encryption with `openssl s_client` to securely submit a password to a local service.


## **Problem Statement**
The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost** using SSL encryption.
OpenSSL is a library for secure communication over networks. It implements the **Transport Layer Security** (TLS) and **Secure Sockets Layer** (SSL) cryptographic protocols that are, for example, used in HTTPS to secure the web traffic.

`openssl s_client` is the implementation of a simple client that connects to a server using SSL/TLS.

### **Task**:
-  Submit the current level's password to port `30001` on `localhost` using **SSL encryption** to retrieve the next password.
  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit15`
  - **Password**: `8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo` 


### **Challenge**:  
- Communication must occur over an encrypted SSL/TLS connection (unlike Level 14’s plaintext `nc` approach). 

---

## 🚀**Solution Approach**
1. **Connect via SSL**: Use `openssl s_client` to establish a secure connection to `localhost:30001`.  
2. **Submit Password**: Send the current password (`8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo`) through the encrypted channel.
---


### **Code Example** 

```bash
# Log into bandit15
ssh bandit15@bandit.labs.overthewire.org -p 2220
```

### Connect to the SSL service and submit the password
```bash
bandit15@bandit:~$ openssl s_client -connect localhost:30001
[SSL connection details...]
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo  # Paste the password and press Enter
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx   # Password for bandit16
```

So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit15.html](https://overthewire.org/wargames/bandit/bandit15.html)

---

## Key Takeaways

- **SSL/TLS Encryption:**
  - Secures data in transit (e.g., passwords) against eavesdropping.
  - Critical for sensitive communications (HTTPS, APIs, etc.).

- **`openssl s_client`:**
  - Command-line tool for testing SSL/TLS connections.
  - Use `-connect <host:port>` to specify the target service.

- **Workflow:**
  - Establish connection → Send password → Receive response.
 
  
## References
- [OverTheWire Bandit Level 15](https://overthewire.org/wargames/bandit/bandit15.html)
- [OpenSSL `s_client` Documentation](https://docs.openssl.org/1.1.1/man1/s_client/)


 ## Additional Notes
 - **Alternative Tools:**
    - Use `ncat --ssl localhost 30001` for a simpler interface.

- **Troubleshooting:**
  - No response? Ensure the password is typed after the SSL handshake completes.
  - Error `Connection refused`? Verify the service is running on port `30001`.

- **SSL Certificate Check:**
  - Use `-verify_return_error` to enforce certificate validation (not needed here).
 

Next Level: [Bandit Level 16 → 17](https://github.com/deejonsen/OverTheWire-Bandit-Games/blob/main/Bandit_Level_16.md)

---


![Screenshot 2025-04-14 185844](https://github.com/user-attachments/assets/d83b9f05-c0f3-448e-b8e2-ec9aea69beb3)
![Screenshot 2025-04-14 185907](https://github.com/user-attachments/assets/3016fa40-8ba7-4796-bf3f-38a4745af10c)
![Screenshot 2025-04-14 190210](https://github.com/user-attachments/assets/acfa6fac-e20f-43cc-8830-68e514fbbc62)
