---
# OverTheWire Bandit Level 1 Walkthrough

---
## **Previous Level:** Level 0

**Login:**

**SSH:** `ssh bandit1@bandit.labs.overthewire.org -p 2220`

**Password:** `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 1 → 2**, focusing on reading a file with a special character in its name.


---

## **Problem Statement**
‘-’ is a special symbol in Linux. So it is not recommended to start a file name with this symbol. ‘-’ is the standard option character. We have already seen it for adding so-called flags for specific options to a command (Like the -p flag for choosing a port for the ssh command.). Because of this, files with this symbol as the first character cannot just be referenced as other files. Get the password from the file called ‘-’.

### **Task**:
- Retrieve the password from a file named `-` in the home directory.
  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit1`  
  - **Password**: `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`


### **Challenge**:  
The filename `-` conflicts with Linux command syntax, where `-` denotes command options/flags (e.g., `cat -` reads from stdin instead of the file).

---

## 🚀**Solution Approach**
1. **List the file**: Confirm the presence of `-` using `ls`.  
2. **Read the file**: Bypass the special character conflict by specifying the file path explicitly with `./-`.

---


### **Code Example**  
```bash
# Connect to the server
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

### **Output**
```bash
bandit1@bandit.labs.overthewire.org's password: [hidden input]
Welcome to OverTheWire!
```

### List files (verify "-" exists)
```bash
bandit1@bandit:~$ ls
-
```

### Read the file using Input Redirection:
```bash
bandit1@bandit:~$ cat < -
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit2.html](https://overthewire.org/wargames/bandit/bandit2.html)

---

## Key Takeaways

**Special Filenames:**
- Avoid filenames starting with `-` in Linux, as they conflict with command options.
-Force Linux to interpret `-` as a file by prefixing it with a path (e.g., `./-` or `/full/path/-`).

**Command Behavior:**
- `cat -` reads from stdin, not the file `-`.

**Input Redirection:**
- Using `< -` explicitly tells the shell to open the file named `-` and feed its contents as standard input (stdin) to the `cat` command..


## References
- [OverTheWire Bandit Level 1](https://overthewire.org/wargames/bandit/bandit1.html)
- [Linux Filename Conventions](https://linux.die.net/man/1/bash)

 ## Additional Notes
 
**Alternative Methods:**
- Use `cat ./` (path resolution; explicitly tells the shell to treat `-` as a file in the current directory).
- Use `cat -- -` (double-dash `--` forces end of command options).

**Troubleshooting:**
- Error `cat: -: No such file or directory`? Ensure you’re in the correct directory (`/home/bandit1`).

Next Level: [Bandit Level 2 → 3](https://github.com/deejonsen/OverTheWire-Bandit-Games/blob/main/Bandit_Level_2.md)
---


![Screenshot 2025-04-13 212548](https://github.com/user-attachments/assets/c80798e2-e22f-460f-89d7-ead949165142)
![Screenshot 2025-04-13 212438](https://github.com/user-attachments/assets/28a1f382-72c9-462d-8484-72853297f80d)
![Screenshot 2025-04-13 212354](https://github.com/user-attachments/assets/558f99b1-214a-486a-8e82-456afb1474a5)
