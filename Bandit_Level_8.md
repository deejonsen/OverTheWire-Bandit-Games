---
# OverTheWire Bandit Level 8 Walkthrough

---
## **Previous Level:** Level 7

**Login:**

**SSH:** `ssh bandit8@bandit.labs.overthewire.org -p 2220`

**Password:** `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 8 → 9**, focusing on identifying a unique line in a file using `sort` and `uniq` commands.

---

## **Problem Statement**
The password for the next level is stored in the file `data.txt` and is the only line of text that occurs only once.
`uniq` is a command that filters input and writes to the output. Specifically, it filters based on identical lines. It has a flag `-u`, which filters for unique lines (lines that appear only ones). Another interesting functionality is, for example, that it can also count (`-c`) or only return duplicate lines (`-d`).

The command is often used with `sort`. For `uniq` to filter for unique lines, the lines need to be sorted. `sort` sorts the lines of a text file. Furthermore, it has flags for sorting in reverse (`-r`) and sorting numerically (`-n`).


### **Task**:
- Find the **only line that occurs once** in the file `data.txt`.
  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit8`  
  - **Password**: `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`


### **Challenge**:  
-`data.txt` contains many lines, with only one unique line (the password).  
- Duplicate lines must be filtered out.

---

## 🚀**Solution Approach**
- **Sort Lines**: Use `sort` to group identical lines consecutively.
- **Filter Unique Line**: Use `uniq -u` to extract the line that appears exactly once.  

---


### **Code Example**  
```bash
# Connect to the server
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

### **Output**
```bash
bandit8@bandit.labs.overthewire.org's password: [hidden input]
Welcome to OverTheWire!
```

###  Sort the file and filter the unique line
```bash
bandit8@bandit:~$ sort data.txt | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit9.html](https://overthewire.org/wargames/bandit/bandit9.html)

---

## Key Takeaways

- **`uniq` Command:**
  - `-u`: Outputs only unique lines (appearing once).
  - Requires **sorted input** to work correctly (identical lines must be consecutive).

- **`sort` Command:**
  - Orders lines alphabetically/numerically to group duplicates.

- **Pipeline (`|`):**
  - Combines `sort` and `uniq` to process large files efficiently.
 

## References
- [OverTheWire Bandit Level 8](https://overthewire.org/wargames/bandit/bandit6.html)
- [Linux `uniq` Manual](https://man7.org/linux/man-pages/man1/uniq.1.html)
- [Linux `sort` Manual](https://man7.org/linux/man-pages/man1/sort.1.html)

 ## Additional Notes
 - **Alternative Methods:**
   - Use `awk` to count occurrences:
```bash
awk '{count[$0]++} END {for (line in count) if (count[line] == 1) print line}' data.txt
```
- **Combine `sort` and `uniq -c` to count duplicates first:**
```bash
sort data.txt | uniq -c | grep "1 "
```

- **Troubleshooting:**
  - Forgot to sort? `uniq -u` will miss duplicates if lines aren’t grouped.
  - Use `wc -l data.txt` to verify the file’s line count.

Next Level: [Bandit Level 9 → 10](https://github.com/deejonsen/OverTheWire-Bandit-Games/blob/main/Bandit_Level_9.md)

---


![Screenshot 2025-04-14 110157](https://github.com/user-attachments/assets/b330f921-808e-4264-bbd8-5ddd28edee02)
![Screenshot 2025-04-14 110039](https://github.com/user-attachments/assets/a58530c0-6b81-4321-97ae-8c147361c623)
![Screenshot 2025-04-14 110012](https://github.com/user-attachments/assets/26fdd089-2f7c-44f5-a3b2-f7bd6dbe2af9)

