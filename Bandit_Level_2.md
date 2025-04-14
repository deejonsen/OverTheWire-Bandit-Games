---
# OverTheWire Bandit Level 2 Walkthrough

---
## **Previous Level:** Level 1

**Login:**

**SSH:** `ssh bandit2@bandit.labs.overthewire.org -p 2220`

**Password:** `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 2 → 3**, focusing on handling filenames with spaces in Linux.


---

## **Problem Statement**
The password for the next level is stored in a file called spaces in this filename located in the home directory. Like in the previous level, it is unconventional and goes against best practice to include spaces in a filename (as well as a directory name). Instead, you can use an underscore (_) or a dash (-).

The reason for this, you can see in the first part of the solution. In a command, spaces indicate a new addition to the command. For example (in the solution), we use the `cat` command, which can take multiple filenames to output text from. And these file names would be separated by space. As can be seen in the solution, instead of outputting the text from the file called ‘spaces in this filename’, it looks for four files called: ‘spaces’, ‘in’, ’this’, ‘filename’.

In case you do encounter a file or directory with space, you have to indicate that the words belong together to one name. This can be done with quotes (single or double), as seen in the solution for this chapter.


### **Task**:
- Retrieve the password from a file named `spaces in this filename` in the home directory.  
  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit2`  
  - **Password**: `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`


### **Challenge**:  
Spaces in filenames are interpreted as argument separators by the shell. For example, `cat spaces in this filename` is parsed as four separate files.

---

## 🚀**Solution Approach**
1. **List the file**: Confirm the filename with `ls`.  
2. **Read the file**: Use quotes or escape characters to treat the entire filename as a single argument.
---


### **Code Example**  
```bash
# Connect to the server
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

### **Output**
```bash
bandit2@bandit.labs.overthewire.org's password: [hidden input]
Welcome to OverTheWire!
```

### List files (verify "spaces in this filename" exists)
```bash
bandit2@bandit:~$ ls
spaces in this filename
```


### Incorrect approach (shell splits the filename)
```bash
bandit2@bandit:~$ cat spaces in this filename
cat: spaces: No such file or directory
cat: in: No such file or directory
cat: this: No such file or directory
cat: filename: No such file or directory
```

### Correct approach 1: Use double quotes
```bash
bandit2@bandit:~$ cat "spaces in this filename"
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

### Correct approach 2: Escape spaces with backslashes
```bash
bandit2@bandit:~$ cat spaces\ in\ this\ filename
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
``` 
So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit3.html](https://overthewire.org/wargames/bandit/bandit3.html)

---

## Key Takeaways

**Filenames with Spaces:**
- The shell splits arguments by spaces. Use quotes (`" "` or `' '`) or escape spaces (`\` ) to preserve filenames as single arguments.

- **Best Practices:**
  - Avoid spaces in filenames; use underscores (`_`) or hyphens (`-`) instead.

- **Shell Parsing:**
  - Commands like `cat` read multiple files if arguments are split (e.g., `cat file1 file2` prints both files).


## References
- [OverTheWire Bandit Level 2](https://overthewire.org/wargames/bandit/bandit2.html)
- [Linux Filename Handling](https://www.gnu.org/software/bash/manual/html_node/Quoting.html))

 ## Additional Notes
 
**Alternative Methods:**
- Use tab completion to auto-escape spaces (type `cat spa<tab>`).
- Wrap the filename in single quotes: `cat 'spaces in this filename'`.

**Troubleshooting:**
- Use `ls -l` to confirm the exact filename.
- Error `No such file or directory`? Check for typos or missing quotes/escape characters.

Next Level: [Bandit Level 3 → 4](https://github.com/deejonsen/OverTheWire-Bandit-Games/blob/main/Bandit_Level_3.md)

---


![Screenshot 2025-04-13 222124](https://github.com/user-attachments/assets/27690498-88bb-481a-bd56-8b64cf84a329)
![Screenshot 2025-04-13 221959](https://github.com/user-attachments/assets/535948c1-49c8-4371-9920-985b719d67f0)
![Screenshot 2025-04-13 221935](https://github.com/user-attachments/assets/31220136-a777-4e9e-b3d9-271a606534fe)
