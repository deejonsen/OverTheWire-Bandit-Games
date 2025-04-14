---
# OverTheWire Bandit Level 12 Walkthrough

---
## **Previous Level:** Level 11

**Login:**

**SSH:** `ssh bandit12@bandit.labs.overthewire.org -p 2220`

**Password:** `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 11 → 12**, focusing on decoding a ROT13-encoded file using the `tr` command to perform character substitution.

---

## **Problem Statement**
The password for the next level is stored in the file **data.txt**, where all lowercase `(a-z)` and uppercase `(A-Z)` letters have been rotated by 13 positions.
**Substitution** means replacing one character with another. Substitution ciphers have been known and used for a very long time. Some of the most known are the Caesar and Vigenère ciphers. However, these simple substitution ciphers are not secure anymore!

As the ‘Helpful Reading Material’ on the levels site mentions, rotating letters by 13 positions is the **ROT13** substitution cipher. It is nice because looking at the Latin alphabet with 26 letters the encryption algorithm equals the decryption algorithm.

The Linux `tr` command, which stands for ’translate’, allows replacing characters with others. The base command syntax looks like the following `tr <old_chars> <new_chars>`.

### **Task**:
- Decode the ROT13-encoded password in `data.txt`.
  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit12`  
  - **Password**: `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`


### **Challenge**:  
- All alphabetic characters in `data.txt` are rotated by 13 positions (ROT13 cipher).
---

## 🚀**Solution Approach**
Use the `tr` command to map characters using ROT13 substitution:  
- **ROT13**: Replace each letter with the one 13 positions ahead in the alphabet (wrapping around).  
- `A-Z` becomes `N-ZA-M`, `a-z` becomes `n-za-m`.
---


### **Code Example**  
```bash
# Connect to the server
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

### **Output**
```bash
bandit11@bandit.labs.overthewire.org's password: [hidden input]
Welcome to OverTheWire!
```

###  Decode ROT13 using tr
```bash
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit12.html](https://overthewire.org/wargames/bandit/bandit12.html)

---

## Key Takeaways

- **ROT13 Cipher:**
  - A substitution cipher where each letter is shifted by 13 positions.
  - **Self-inverse:** Encoding and decoding use the same algorithm (e.g., `tr 'A-Za-z' 'N-ZA-Mn-za-m'`).

- **`tr` Command:**
  - Translates or deletes characters (e.g., `tr <old_chars> <new_chars>`).

- **Alias Tip:**
  - Create shortcuts for common ciphers:
```bash
alias rot13="tr 'A-Za-z' 'N-ZA-Mn-za-m'"  # ROT13 for letters
alias rot5="tr '0-9' '5-90-4'"             # ROT5 for numbers
 ```

## References
- [OverTheWire Bandit Level 11](https://overthewire.org/wargames/bandit/bandit11.html)
- [Linux `tr` Command Guide](https://man7.org/linux/man-pages/man1/tr.1.html)


 ## Additional Notes
 - **Alternative Methods:**
   - Use online ROT13 decoders (e.g., rot13.com).
   - Decode with Python:

```python
python3 -c "import codecs; print(codecs.decode('Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh', 'rot_13'))"
```
- **Troubleshooting:**
  - Ensure case sensitivity: `A-Za-z` covers uppercase and lowercase.
  - Verify no typos in the `tr` substitution pattern.

Next Level: Bandit Level 11 → 12

---


![Screenshot 2025-04-14 123554](https://github.com/user-attachments/assets/52b8d2a2-be0e-4c8d-8b7e-73f0f7abd29b)
![Screenshot 2025-04-14 123415](https://github.com/user-attachments/assets/1a777047-c6f2-43ba-a21b-0f52ab7e4498)
![Screenshot 2025-04-14 123351](https://github.com/user-attachments/assets/a03b7d62-881e-4595-8fc6-00fdfb285990)
