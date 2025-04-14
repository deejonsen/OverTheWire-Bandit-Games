---
# OverTheWire Bandit Level 6 Walkthrough

---
## **Previous Level:** Level 5

**Login:**

**SSH:** `ssh bandit6@bandit.labs.overthewire.org -p 2220`

**Password:** `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 6 → 7**, focusing on locating a file with specific ownership and size criteria using the `find` command in Linux.

---

## **Problem Statement**
Find a file somewhere on the server with the following properties:
  - Owned by user **bandit7**
  - Owned by group **bandit6**
  - **33 bytes** in size

In this level, we are introduced to the big topic of Linux **File Permissions**. Specifically, to the area of **ownership**. Each file is owned by a user and a group. You can see what user and group owns a file with the `ls` command and its `-l` tag.

Example:
```bash
1. bandit6@bandit:/var/lib/dpkg/info$ ls -l bandit7.password 
2. -rw-r----- 1 bandit7 bandit6 33 May  7  2020 bandit7.password
```
The second column shows the user, the third shows the group that owns the file.

As mentioned in a previous level, the `find` command can be used to find files on the server. It offers flags to look for files owned by a specific user (`-user <username>`) and a specific group (`-group <groupname>`)

### **Task**:
- Find a file somewhere on the server with the following properties:
  - Owned by user **bandit7**
  - Owned by group **bandit6**
  - **33 bytes** in size

  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit6`  
  - **Password**: `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`


### **Challenge**:  
- The file exists somewhere on the entire filesystem, not just the home directory.  
- Permission errors clutter output when searching system-wide.


---

## 🚀**Solution Approach**
**Use the `find` command with flags to filter files by:**
1. **Ownership**: `-user bandit7` (user) and `-group bandit6` (group).  
2. **Size**: `-size 33c` (33 bytes).  
3. **Type**: `-type f` (files only).  

Suppress permission errors with `2>/dev/null`.
---


### **Code Example**  
```bash
# Connect to the server
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

### **Output**
```bash
bandit6@bandit.labs.overthewire.org's password: [hidden input]
Welcome to OverTheWire!
```

### Search the entire filesystem with error suppression
```bash
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
```

### Read the file
```bash
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```


So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit7.html](https://overthewire.org/wargames/bandit/bandit7.html)

---

## Key Takeaways

- **Linux Ownership:**
  - Files are owned by a user and group. Use `ls -l` to view ownership.
  - Example: `-rw-r----- 1 bandit7 bandit6` → User: `bandit7`, Group: `bandit6`.

- **`find` Command:**
  - `-user <name>`: Filter by user ownership.
`- `-group <name>`: Filter by group ownership.
  - `-size <n>c`: Match exact size in bytes (e.g., `33c`).

- **Error Suppression:**
  - `2>/dev/null` redirects stderr (error messages) to the void, cleaning up output.

## References
- [OverTheWire Bandit Level 6](https://overthewire.org/wargames/bandit/bandit6.html)
- [Linux `find` Command Guide](https://man7.org/linux/man-pages/man1/find.1.html))

 ## Additional Notes
 - Why Start at `/`?: Searching from root (`/`) ensures all directories are scanned.

**Troubleshooting:**
- `Permission denied`? Use `sudo` if allowed (not needed here).
- Typos in ownership names? Double-check with `id bandit7` or `groups bandit6`.

Next Level: [Bandit Level 7 → 8](https://github.com/deejonsen/OverTheWire-Bandit-Games/blob/main/Bandit_Level_7.md)

---


![Screenshot 2025-04-14 100724](https://github.com/user-attachments/assets/e64bc338-fff7-4d18-9fcb-00d7fa8edc03)
![Screenshot 2025-04-14 100350](https://github.com/user-attachments/assets/afb28d3f-49b0-422a-ba81-49b5d5c39ef0)
![Screenshot 2025-04-14 100318](https://github.com/user-attachments/assets/fba98930-a7da-480c-b6a0-03b57006a347)

