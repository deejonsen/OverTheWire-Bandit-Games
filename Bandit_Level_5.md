---
# OverTheWire Bandit Level 5 Walkthrough

---
## **Previous Level:** Level 4

**Login:**

**SSH:** `ssh bandit5@bandit.labs.overthewire.org -p 2220`

**Password:** `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 5 → 6**, focusing on advanced file searching using `find`, `file`, and `grep` to locate a file with specific properties (size, readability, and permissions).


---

## **Problem Statement**
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
  - human-readable
  - 1033 bytes in size
  - not executable

An introduction to the `file` command and how to used it to detect **human-readable** files was given in Level 4. The `file` command alone worked well for a small number of files. However, with more files, it is easy to lose the overview.

The command `grep` searches its input for lines containing a specific pattern defined by the user. It can also be used to do the opposite, meaning when using the `-v` flag, a line with a defined pattern will not be printed.

To use this command on the output of another command (for example, the `file` command), we use the pipe `|`. It takes the output of the first command and pipes it as input into the second command. The syntax could look something like this: `<command1> | grep <pattern>`.


To get the file size, we use the `du` command. Specifically, to get the size in bytes, we also use the `-b` flag. To look at all the files, including hidden ones, the `-a` flag is offered.

Addition: The `ls -l` command also shows the size of files in the fifth column.


For finding **non-executable** files, the `find` command can be used. It has the `-executable` flag, which searches for executable files and allows operators like `‘!’` for negation.

Some additional interesting flags for `find`:

It has a flag for looking at file size in bytes `-size <bytes>`.
It also has the option to only look at files `-type f` (no directories/non-executables).
It has a `-readable` flag, but this means you have the permission to read the files, not that they are human-readable.
Instead, we could use the `-exec <command>` flag with `'{}'` as a path, meaning the chosen command will be executed on all the files. This could be used to execute another command like `file`.


### **Task**:
- Find the password in a file under the `inhere` directory with the following properties:  
  - **Human-readable** (ASCII/Unicode).  
  - **1033 bytes** in size.  
  - **Not executable**.

  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit5`  
  - **Password**: `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`


### **Challenge**:  
- The `inhere` directory contains 20 subdirectories (`maybehere00` to `maybehere19`), each with multiple files.  
- Manually checking each file is impractical.  


---

## 🚀**Solution Approach**
**Method 1: Step-by-Step Filtering**  
1. **Find human-readable files:** 
   ```bash
   file */{.,}* | grep "ASCII text"
   ```

2. **Filter by size (1033 bytes):**
```bash
du -b -a | grep 1033
```

3. **Verify non-executable status:**
```bash
find . ! -executable  
```


**Method 2: Single `find` Command:**
- Use `find` with flags to combine all criteria:

```bash
find . -type f -size 1033c ! -executable -exec file '{}' \; | grep ASCII
```

---


### **Code Example**  
```bash
# Connect to the server
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

### **Output**
```bash
bandit5@bandit.labs.overthewire.org's password: [hidden input]
Welcome to OverTheWire!
```

### Navigate to the directory
```bash
bandit5@bandit:~$ cd inhere
```


### Method 1: Step-by-Step:
1. **List human-readable files:**
```bash
bandit5@bandit:~/inhere$ file */{.,}* | grep "ASCII text"
maybehere10/.file2:       ASCII text
maybehere15/.file2:       ASCII text
maybehere01/-file2:       ASCII text
```

2. **Check file sizes (1033 bytes):**
```bash
bandit5@bandit:~/inhere$ du -b -a | grep 1033
1033    ./maybehere07/.file2bash
```

3. **Confirm non-executable status:**
```bash
bandit5@bandit:~/inhere$ find . ! -executable | grep maybehere07/.file2
./maybehere07/.file2
```

4. **Read the file:**
```bash
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```


### Method 2: One Command:
```bash
bandit5@bandit:~/inhere$ find . -type f -size 1033c ! -executable -exec file '{}' \; | grep ASCII
./maybehere07/.file2: ASCII text, with very long lines
```

```bash
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit6.html](https://overthewire.org/wargames/bandit/bandit6.html)

---

## Key Takeaways

- **`find` Command:**
  - `size 1033c`: Matches files of exact size (1033 bytes).
  - `-type f`: Filters only files (not directories).
  - `! -executable`: Excludes executable files.
  - `-exec file '{}' \;`: Runs `file` on each result.

- **Efficiency:**
  - Combining criteria in `find` avoids manual filtering.

- **Wildcards:**
  - `*/{.,}*` matches both hidden and non-hidden files in subdirectories.


## References
- [OverTheWire Bandit Level 5](https://overthewire.org/wargames/bandit/bandit5.html)
- [Linux `find` Command Guide](https://man7.org/linux/man-pages/man1/find.1.html)

 ## Additional Notes
 - Why `-size 1033c`?: The `c` suffix specifies bytes.

**Troubleshooting:**
- Use `ls -l` to check file permissions (e.g., `-rw-r--r--` = non-executable).
- Error `Permission denied`? Ensure you’re in the `inhere` directory.

Next Level: Bandit Level 6 → 7

---


![Screenshot 2025-04-14 083256](https://github.com/user-attachments/assets/fa5299ac-b98d-40e7-8744-1e9ff65a1f03)
![Screenshot 2025-04-14 082747](https://github.com/user-attachments/assets/ceb34a39-5bca-479d-8b8f-c6132999926b)
![Screenshot 2025-04-14 082643](https://github.com/user-attachments/assets/1e75bf71-71ff-40eb-a08e-6a05a4bd4a61)
![Screenshot 2025-04-14 082411](https://github.com/user-attachments/assets/ad635974-edf7-4b76-9e28-192c089c8caa)
![Screenshot 2025-04-14 081947](https://github.com/user-attachments/assets/707b0bf8-b411-42c9-ae2d-cb1ed6c31ad7)
![Screenshot 2025-04-14 081814](https://github.com/user-attachments/assets/52288424-7a26-4d93-bfe3-ed8bfcd09fa6)
![Screenshot 2025-04-14 081746](https://github.com/user-attachments/assets/ffba778b-670e-4247-97d1-333bf5638804)
