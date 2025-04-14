---
# OverTheWire Bandit Level 10 Walkthrough

---
## **Previous Level:** Level 9

**Login:**

**SSH:** `ssh bandit10@bandit.labs.overthewire.org -p 2220`

**Password:** `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey`


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 10 → 11**, focusing on decoding a Base64-encoded file using the `base64` command in Linux.

---

## **Problem Statement**
The password for the next level is stored in the file data.txt, which contains base64 encoded data.

**Base64** is a binary-to-text encoding scheme. It can often be recognised by equal signs at the end of the data. However, this is not always the case. Linux has a command called `base64` that allows for encoding and decoding in Base64. For decoding, we need to use the flag `-d`.

### **Task**:
- Decode the Base64-encoded data in `data.txt` to retrieve the password.
  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit10`  
  - **Password**: `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey`


### **Challenge**:  
- `data.txt` contains a Base64-encoded string (`VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg==`).
---

## 🚀**Solution Approach**
- Use the `base64 -d` command to decode the file. The `-d` flag specifies decoding mode.

---


### **Code Example**  
```bash
# Connect to the server
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

### **Output**
```bash
bandit10@bandit.labs.overthewire.org's password: [hidden input]
Welcome to OverTheWire!
```

###  View the encoded content
```bash
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg==
```

### Decode the Base64 data
```bash
bandit10@bandit:~$ base64 -d data.txt
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit11.html](https://overthewire.org/wargames/bandit/bandit11.html)

---

## Key Takeaways

- **Base64 Encoding:**
  - A method to encode binary data into ASCII text.
  - Often identified by trailing `=` characters (padding).

- **`base64` Command:**
  - `-d`: Decodes the input (default is encoding).
  - Can read directly from files or stdin.
 

## References
- [OverTheWire Bandit Level 10](https://overthewire.org/wargames/bandit/bandit10.html)
- [Linux `base64` Manual](https://man7.org/linux/man-pages/man1/base64.1.html)

 ## Additional Notes
 - **Alternative Methods:**
   - Use online Base64 decoders (not recommended for sensitive data).
   - Decode from stdin: `echo "<encoded_string>" | base64 -d`.

- **Troubleshooting:**
  - Error `invalid input`? Ensure the string is properly padded (e.g., with `=`).
  - Use `file data.txt` to confirm the file is text (not binary).


Next Level: [Bandit Level 11 → 12](https://github.com/deejonsen/OverTheWire-Bandit-Games/blob/main/Bandit_Level_11.md)

---


![Screenshot 2025-04-14 115649](https://github.com/user-attachments/assets/e5999d61-7a3f-4919-bce9-43f62c23e99d)
![Screenshot 2025-04-14 115536](https://github.com/user-attachments/assets/e1e16aed-5c5a-4511-b156-04131ad49930)
![Screenshot 2025-04-14 115454](https://github.com/user-attachments/assets/28591b3d-8657-4d52-875e-5317786da8a3)

