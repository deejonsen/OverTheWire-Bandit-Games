---
# OverTheWire Bandit Level 3 Walkthrough

---
## **Previous Level:** Level 2

**Login:**

**SSH:** `ssh bandit3@bandit.labs.overthewire.org -p 2220`

**Password:** `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 3 → 4**, focusing on accessing hidden files and directory navigation in Linux.


---

## **Problem Statement**
The password for the next level is stored in a hidden file in the inhere directory. To traverse the directories, the “change directory” command exists: `cd <path>`.

The path for the command can be an absolute path (path from root directory `/`) or a relative path (path from the current working directory).

Interesting uses of the command are:

`cd ..` goes to the parent directory
`cd /` goes to the root directory
`cd ~` goes to the home directory (of the current user)

A hidden file in Linux starts with a `.`. The `ls` command shows only non-hidden files. However, with the `-a` flag it shows all files, specifically also the hidden files.

The first two hidden entries in the directories stand for the current (`.`) and the parent (`..`) directory.

### **Task**:
- Retrieve the password from a hidden file named `.hidden` located in the `inhere` directory.  
  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit3`  
  - **Password**: `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`


### **Challenge**:  
- Hidden files in Linux start with `.` and are not displayed by default using `ls`.  
- Navigating directories requires understanding absolute/relative paths.

---

## 🚀**Solution Approach**

### **Method 1: Directory Traversal**:  
1. Navigate to the `inhere` directory using `cd`.  
2. List **all** files (including hidden ones) with `ls -la`.  
3. Read the hidden file using `cat`.


### **Method 2: Without Traversal**  
1. Access the file directly by specifying its relative path (`inhere/.hidden`).  

---


### **Code Example**  
```bash
# Connect to the server
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

### **Output**
```bash
bandit3@bandit.labs.overthewire.org's password: [hidden input]
Welcome to OverTheWire!
```

## --- Method 1: Directory Traversal ---
### Navigate to the Directory
```bash
bandit3@bandit:~$ cd inhere
```

## List all files (including hidden)
```bash
bandit3@bandit:~/inhere$ ls -la
...Hiding-From-You
```

## Read the hidden file
```bash
bandit3@bandit:~/inhere$ cat "...Hiding-From-You"
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

## --- Method 2: Direct Path ---
### Access the File Without Changing Directories

```bash
bandit3@bandit:~$ cat inhere/. ...Hiding-From-You
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```


So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit4.html](https://overthewire.org/wargames/bandit/bandit4-.html)

---

## Key Takeaways

- **Hidden Files:**
  - Files starting with `.` are hidden. Use `ls -la` to display them.
  - Common hidden files: `.bashrc`, `.ssh`, `.gitignore`.

- **Directory Navigation:**
  - `cd <path>`: Change directory using absolute (`/path/to/dir`) or relative (`../parent_dir`) paths.
  - Shortcuts: `cd ~` (home), `cd ..` (parent directory), `cd -` (previous directory).

- **Path Specification:**
  - Access files in subdirectories without navigating there (e.g., `cat dir/file`).



## References
- [OverTheWire Bandit Level 3](https://overthewire.org/wargames/bandit/bandit3.html)
- [Linux Hidden Files](https://linuxize.com/post/how-to-list-show-hidden-files-and-directories-in-linux/)


 ## Additional Notes
 
**Why Hidden Files?:** Often used for configuration files to reduce clutter.

**Troubleshooting:**
- Can’t find `...Hiding-From-You`? Ensure you’re in the correct directory (`/home/bandit3/inhere`).
- Use `pwd` to confirm your current directory.



Next Level: Bandit Level 4 → 5

---

![Screenshot 2025-04-13 225618](https://github.com/user-attachments/assets/3cc8a89b-255b-47a5-9322-874df3bf7e7d)
![Screenshot 2025-04-13 225355](https://github.com/user-attachments/assets/5abd285b-9b3a-4552-b4ec-41b2b9107e67)
![Screenshot 2025-04-13 225331](https://github.com/user-attachments/assets/8a34cc77-09a1-4780-858b-3e1939c8dc9f)


