---
# OverTheWire Bandit Level 7 Walkthrough

---
## **Previous Level:** Level 6

**Login:**

**SSH:** `ssh bandit7@bandit.labs.overthewire.org -p 2220`

**Password:** `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 7 → 8**, focusing on efficiently extracting a password adjacent to a specific keyword (`millionth`) in a large file using `grep`.

---

## **Problem Statement**
Get the password from a file, next to the word **millionth**.

As mentioned in a previous level, `grep` can be used to search lines that contain a specific pattern like follow `grep <pattern>`.

With the pipe (`|`), we can pipe the output of `cat` to `grep` as input to look through a text file.


### **Task**:
- Retrieve the password located **next to the word "millionth"** in the file `data.txt`.
  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit7`  
  - **Password**: `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`


### **Challenge**:  
- `data.txt` is **4.1 MB** in size (too large to manually search).  
- The password is on the same line as the keyword `millionth`.

---

## 🚀**Solution Approach**
- Use `grep` to search for the keyword `millionth` in `data.txt`, leveraging its ability to filter lines containing a specific pattern.

---


### **Code Example**  
```bash
# Connect to the server
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

### **Output**
```bash
bandit7@bandit.labs.overthewire.org's password: [hidden input]
Welcome to OverTheWire!
```

###  Search for the keyword "millionth" in data.txt
```bash
bandit7@bandit:~$ du -b data.txt
4184396 data.txt
```

```bash
bandit7@bandit:~$ cat data.txt | grep millionth
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit8.html](https://overthewire.org/wargames/bandit/bandit8.html)

---

## Key Takeaways

- **`grep` Command:**
  - Efficiently searches for patterns in text files.
  - Syntax: `grep <pattern> <file>` or `cat <file> | grep <pattern>`.

- **Handling Large Files:**
  - Avoid manual searches; use tools like `grep`, `awk`, or `sed`.

- **Pipes (`|`):**
  - Redirect the output of one command (e.g., `cat`) as input to another (e.g., `grep`).
 

## References
- [OverTheWire Bandit Level 6](https://overthewire.org/wargames/bandit/bandit6.html)
- [Linux `grep` Guide](https://www.gnu.org/software/grep/manual/grep.html)

 ## Additional Notes
 - **Alternative Methods:**
   - Use `less data.txt` + `/millionth` to search interactively.
   - Use `awk '/millionth/ {print $2}' data.txt` to extract the second field.

- **Troubleshooting:**
  - Ensure the keyword is spelled correctly (case-sensitive).
  - Use `wc -l data.txt` to count lines if unsure about the file’s structure.


Next Level: Bandit Level 8 → 9

---


![Screenshot 2025-04-14 103344](https://github.com/user-attachments/assets/a4e0be85-b44c-4b51-b20a-241878594854)
![Screenshot 2025-04-14 102927](https://github.com/user-attachments/assets/11dd33d2-d309-4c85-acc9-f7b035ea20ba)
![Screenshot 2025-04-14 102907](https://github.com/user-attachments/assets/6308646e-26cb-4957-8375-1aedae9edeec)

