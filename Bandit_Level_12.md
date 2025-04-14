---
# OverTheWire Bandit Level 12 Walkthrough

---
## **Previous Level:** Level 11

**Login:**

**SSH:** `ssh bandit12@bandit.labs.overthewire.org -p 2220`

**Password:** `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 12 → 13**, focusing on reversing a hexdump and recursively decompressing a multi-layered file using `xxd`, `gzip`, `bzip2`, and `tar`.

---

## **Problem Statement**
The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level, it may be useful to create a directory under /tmp in which you can work using mkdir.
- `mkdir <path>` can be used to create a new directory.
- `cp <source> <destination>` copies files.
- `mv <source> <destination>` moves or renames files.

**Hexdumps** are often used when we want to look at data that cannot be represented in strings and therefore is not readable, so it is easier to look at the hex values. A hexdump has three main columns. The first shows the address, the second the hex representation of the data on that address and the last shows the actual data as strings (with ‘.’ being hex values that cannot be represented as a string). Many hex editors exist just pick the one you like most.

For the command line `xxd` can be used. `xxd <input_file> <output_file>` creates hexdumps. When using the `-r` flag, it reverts the hexdump.

Hexdumps can be used to figure out the type of a file. Each file type has a **magic number/file signature**. You can find lists with a collection of these different file signatures online. The file command, which was introduced in Level 5 also uses this method (and more beyond that). This is especially important to know because sometimes files might not have the correct or any file ending to identify its type.


Compression is a method of encoding that aims to reduce the original size of a file without losing information (or only losing as little as possible).

`gzip` is a command to compress or decompress (`-d`) files. A `‘gzip’` file generally ends with .gz.
`bzip2` is another command which allows for compressing and decompressing (`-d`) files. A ‘bzip2’ file generally ends with `.bz2`.
An **Archive File** is a file that contains one or multiple files and their metadata. This can allow easier portability.

`tar` is a command that creates archive files (`-cf`). It also allows extracting these files again (`-xf`). A tar archive generally ends with `.tar`.


### **Task**:
- Retrieve the password from `data.txt`, a hexdump of a file compressed multiple times with different algorithms.
  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit12`  
  - **Password**: `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`


### **Challenge**:  
- The file is hexdumped, then compressed with `gzip`, `bzip2`, and archived with `tar` **multiple times**.

---

## 🚀**Solution Approach**
1. **Workspace Setup**: Create a temporary directory to avoid cluttering the home folder.  
2. **Hexdump Reversal**: Use `xxd -r` to convert the hexdump back to binary.  
3. **Recursive Decompression**: Identify file types via magic numbers and decompress iteratively.  

---


### **Code Example**  
```bash
# Connect to the server
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

### **Output**
```bash
bandit12@bandit.labs.overthewire.org's password: [hidden input]
Welcome to OverTheWire!
```

###  Create a Temporary Workspace
```bash
bandit12@bandit:~$ cd /tmp
bandit12@bandit:~$ mktemp -d
bandit12@bandit:~$ cd /tmp/tmp.9WKv0MOmR4
bandit12@bandit:/tmp/tmp.9WKv0MOmR4$ cp ~/data.txt .
bandit12@bandit:/tmp/tmp.9WKv0MOmR4$ mv data.txt hexdump_data
```

### Revert the Hexdump to Binary
```bash
bandit12@bandit:/tmp/tmp.9WKv0MOmR4$ xxd -r hexdump_data > compressed_data
```

### Decompress layers (gzip → bzip2 → tar → ... → gzip)
```bash
bandit12@bandit:/tmp/tmp.9WKv0MOmR4$ mv compressed_data compressed.gz
bandit12@bandit:/tmp/tmp.9WKv0MOmR4$ gzip -d compressed.gz
bandit12@bandit:/tmp/tmp.9WKv0MOmR4$ mv compressed compressed.bz2
bandit12@bandit:/tmp/tmp.9WKv0MOmR4$ bzip2 -d compressed.bz2
bandit12@bandit:/tmp/tmp.9WKv0MOmR4$ tar -xf compressed
bandit12@bandit:/tmp/tmp.9WKv0MOmR4$ tar -xf data5.bin
bandit12@bandit:/tmp/tmp.9WKv0MOmR4$ bzip2 -d data6.bin
bandit12@bandit:/tmp/tmp.9WKv0MOmR4$ tar -xf data6.bin.out
bandit12@bandit:/tmp/tmp.9WKv0MOmR4$ mv data8.bin data8.gz
bandit12@bandit:/tmp/tmp.9WKv0MOmR4$ gzip -d data8.gz
```

### Get the password
```bash
bandit12@bandit:/tmp/tmp.9WKv0MOmR4$ cat data8
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit13.html](https://overthewire.org/wargames/bandit/bandit13.html)

---

## Key Takeaways

- **Hexdump Handling:**
  - Use `xxd -r` to revert hexdumps to binary.
  - Magic numbers (e.g., `1f8b` for gzip, `425a` for bzip2) identify file types.

- **Decompression Tools:**
  - `gzip -d`, `bzip2 -d`, and `tar -xf` for layered extraction.

- **File Signatures:**
  - Check headers with `xxd | head` or `file <filename>` to determine compression type.

## References
- [OverTheWire Bandit Level 12](https://overthewire.org/wargames/bandit/bandit12.html)
- [Linux `xxd` Manual](https://linux.die.net/man/1/xxd)
- [File Signatures List](https://en.wikipedia.org/wiki/List_of_file_signatures)


 ## Additional Notes
 - **Alternative Workflow:**
    - Use `file` to auto-detect compression type at each step:

```bash
file compressed_data | awk '{print $2}' # Returns "gzip", "bzip2", etc.
```

- **Troubleshooting:**
  - Permission denied? Use `chmod 700 /tmp/your_dir`.
  - Use `ls -l` to track file ownership after extraction.

Next Level: [Bandit Level 13 → 14](https://github.com/deejonsen/OverTheWire-Bandit-Games/blob/main/Bandit_Level_13.md)

---


![Screenshot 2025-04-14 162135](https://github.com/user-attachments/assets/b7eaea28-645a-4707-a31e-53390020731f)
![Screenshot 2025-04-14 162206](https://github.com/user-attachments/assets/8aa76960-614c-4a61-8667-5b512c04044a)
![Screenshot 2025-04-14 162453](https://github.com/user-attachments/assets/bcb6c208-bf0a-41da-b865-942140e09c95)
![Screenshot 2025-04-14 162514](https://github.com/user-attachments/assets/de1e4d3f-07ac-4fc6-9b8b-38f0957c6031)
![Screenshot 2025-04-14 164531](https://github.com/user-attachments/assets/3b1bbe84-1772-4d17-9101-e9d8ff706ab4)
![Screenshot 2025-04-14 164541](https://github.com/user-attachments/assets/0465c750-1441-486f-83e6-c3c0fae4566e)
![Screenshot 2025-04-14 164804](https://github.com/user-attachments/assets/467b7d8f-66ae-478f-b8cd-96cf1c267b40)
![Screenshot 2025-04-14 164816](https://github.com/user-attachments/assets/fb38b8de-6b90-41a8-b7d5-25867a6206cf)
![Screenshot 2025-04-14 165036](https://github.com/user-attachments/assets/3ece604c-e462-4d25-9b4c-fb35556e0563)
![Screenshot 2025-04-14 165108](https://github.com/user-attachments/assets/c6cf498c-ba89-4390-ba0a-c27d9fa1db41)
![Screenshot 2025-04-14 165145](https://github.com/user-attachments/assets/afdf1cb0-1f52-418b-b070-d5f75c67a28f)
![Screenshot 2025-04-14 165426](https://github.com/user-attachments/assets/fcb07c72-e53d-4058-a19b-f01416c7afe0)
![Screenshot 2025-04-14 165623](https://github.com/user-attachments/assets/cba97f95-09f5-4c5b-a37c-302f5cf58528)
![image](https://github.com/user-attachments/assets/209b1f6e-0f93-4cc0-9d9d-dcdb389bf59d)
