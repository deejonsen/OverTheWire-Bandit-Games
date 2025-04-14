---
# OverTheWire Bandit Level 4 Walkthrough

---
## **Previous Level:** Level 3

**Login:**

**SSH:** `ssh bandit4@bandit.labs.overthewire.org -p 2220`

**Password:** `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 4 → 5**, focusing on identifying human-readable files using the `file` command and wildcards in Linux.


---

## **Problem Statement**
The password for the next level is stored in the only human-readable file in the inhere directory. The `file` command gives us the type of data of the file. Some examples would be: ‘ELF’, ‘Perl script’, ‘ASCII text’, ‘data’ and more.

For this task, we are looking specifically for `human-readable` files. It means that the data is presented so that we can read the information. An ELF file, for example, is not human-readable. If you would try to print its content (`head <elf_file_name>`), the result would look something like this: `�������$��$,0�%��0�'��0<u���8�w���9�t�`.

The most common data encodings that are human-readable are ASCII and Unicode.

If we want to apply/use a command on all the files in the current directory, repeating the command or writing all filenames is tedious. To use the command on all the files in the directory without a lot of writing, we can use ‘*’, which is called a ‘wildcard symbol’. ‘*’ can stand for any number of any literal characters. An example could be `file*`, which would match to everything that starts with `‘file’`, like `‘file00’`, `‘file’`, `‘fileAA’` and so on. It replaces the filename/path option in the command.


### **Task**:
- Find the password in the **only human-readable file** within the `inhere` directory.  
  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit4`  
  - **Password**: `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`


### **Challenge**:  
- Ten files exist in `inhere`, all starting with `-` (e.g., `-file00`, `-file01`).  
- Only **one file** contains ASCII text (human-readable), while others are binary/data files. 

---

## 🚀**Solution Approach**

1. **List Files**: Navigate to `inhere` and confirm filenames with `ls`.  
2. **Identify File Types**: Use `file ./*` to detect the human-readable file (ASCII text).  
3. **Read the File**: Access the correct file using `./-file07` to bypass the `-` filename issue.  

---


### **Code Example**  
```bash
# Connect to the server
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

### **Output**
```bash
bandit4@bandit.labs.overthewire.org's password: [hidden input]
Welcome to OverTheWire!
```

### Navigate to the Directory
```bash
bandit4@bandit:~$ cd inhere
```

### List all files (note filenames start with '-')
```bash
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```

#### Check file types using wildcard (*)
```bash
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text  # <--- Target file!
./-file08: data
./-file09: data
```

## Read the ASCII file
```bash
bandit4@bandit:~/inhere$ cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit5.html](https://overthewire.org/wargames/bandit/bandit5-.html)

---

## Key Takeaways

- **`file` Command:**
  - Determines a file’s type (e.g., `ASCII text`, `ELF binary`, `data`).
  - Human-readable files typically show `ASCII` or `Unicode`.

- **Wildcards (`*`):**
  - `./*` matches all files in the current directory.
  - Avoids manually typing filenames, especially useful for bulk operations.

- **Special Filenames:**
  - Prefix filenames starting with `-` with `./` (e.g., `./-file07`) to prevent command misinterpretation.



## References
- [OverTheWire Bandit Level 4](https://overthewire.org/wargames/bandit/bandit4.html)
- [Linux Wildcards Guide](https://tldp.org/LDP/GNU-Linux-Tools-Summary/html/x11655.htm))


 ## Additional Notes
 
- **Alternative Methods:**
  - Use `find . -type f -exec file {} \;` to check all files recursively.
  - Redirect output to a file for analysis: `file ./* > results.txt`.

- **Troubleshooting:**
  - Error `Permission denied`? Ensure you’re logged in as `bandit4`.
  - Use `head -n 1 <file>` to preview non-ASCII files safely.



Next Level: Bandit Level 5 → 6

---

![Screenshot 2025-04-14 005208](https://github.com/user-attachments/assets/5f972348-f952-47b9-8aee-e485c5b52f20)
![Screenshot 2025-04-14 005117](https://github.com/user-attachments/assets/301d4df2-d4a8-4d78-8fdf-8a32fd8f5ec3)
![Screenshot 2025-04-14 004947](https://github.com/user-attachments/assets/4ced292e-f118-41e7-8965-4e23f096864e)
![Screenshot 2025-04-14 004806](https://github.com/user-attachments/assets/33ff05eb-4f16-4c4a-8e9f-cf709081848f)


