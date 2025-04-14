---
# OverTheWire Bandit Level 9 Walkthrough

---
## **Previous Level:** Level 8

**Login:**

**SSH:** `ssh bandit9@bandit.labs.overthewire.org -p 2220`

**Password:** `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 9 → 10**, focusing on extracting human-readable strings from a binary file and identifying patterns using `strings` and `grep`.

---

## **Problem Statement**
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.
The `strings` command finds human-readable strings in files. Specifically, it prints sequences of printable characters. Its main use is for non-printable files like hex dumps or executables.

### **Task**:
- Retrieve the password from `data.txt`, located in a human-readable string preceded by **multiple '=' characters**.
  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit9`  
  - **Password**: `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`


### **Challenge**:  
- `data.txt` contains non-printable characters (not a plain text file).  
- The password is embedded in a human-readable string surrounded by `=` symbols.

---

## 🚀**Solution Approach**
- **Extract Human-Readable Strings**: Use `strings` to filter printable sequences.  
2. **Filter Lines with '=' Symbols**: Use `grep` to isolate lines containing `===` (or similar patterns).
  
---


### **Code Example**  
```bash
# Connect to the server
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

### **Output**
```bash
bandit9@bandit.labs.overthewire.org's password: [hidden input]
Welcome to OverTheWire!
```

###  Extract readable strings and filter for lines with '==='
```bash
bandit9@bandit:~$ strings data.txt | grep "==="
========== the*2i"4
========== password
Z)========== is
&========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit10.html](https://overthewire.org/wargames/bandit/bandit10.html)

---

## Key Takeaways

- **`strings` Command:**
  - Extracts human-readable sequences from binary/non-text files.
  - Critical for analyzing executables, logs, or encoded data.

- **`grep` with Patterns:**
  - Use regex (`grep "===+"`) or literal patterns (`grep "==="`) to filter lines.

- **Pattern Flexibility:**
  - The exact number of `=` symbols isn’t specified, but `===` suffices here.
 

## References
- [OverTheWire Bandit Level 9](https://overthewire.org/wargames/bandit/bandit9.html)
- [Linux `strings` Command Guide](https://man7.org/linux/man-pages/man1/strings.1.html)

 ## Additional Notes
 - **Alternative Methods:**
   - Use `hexdump -C data.txt` to inspect raw bytes, then search for patterns.
   - Refine the regex: `strings data.txt | grep -E "=+"`.

- **Troubleshooting:**
  - No output? Adjust the number of `=` symbols (e.g., `grep "=="`).
  - Use `head data.txt` to confirm the file is non-text.
 

Next Level: Bandit Level 10 → 11

---


![Screenshot 2025-04-14 112806](https://github.com/user-attachments/assets/cfffe091-68fc-4edc-9ff1-730c8321b599)
![Screenshot 2025-04-14 112759](https://github.com/user-attachments/assets/2a0f21fc-16a6-4a88-8cb8-0849f6725873)
![Screenshot 2025-04-14 112712](https://github.com/user-attachments/assets/609acfc7-4a97-4424-96c1-eb35cb2cecc1)
![Screenshot 2025-04-14 112641](https://github.com/user-attachments/assets/59bef085-9bfa-4333-9bd6-9590f212105e)
![Screenshot 2025-04-14 112431](https://github.com/user-attachments/assets/793c7ab7-565c-47c1-9faa-28f74e246caf)
![Screenshot 2025-04-14 112330](https://github.com/user-attachments/assets/35a4c2a3-9a30-4dea-b4da-a09e0d688e9b)

