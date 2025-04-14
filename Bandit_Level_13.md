---
# OverTheWire Bandit Level 13 Walkthrough

---
## **Previous Level:** Level 12

**Login:**

**SSH:** `ssh bandit13@bandit.labs.overthewire.org -p 2220`

**Password:** `FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn`


## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 13 → 14**, focusing on using an **SSH private key** to authenticate into the next level and retrieve the password.
---

## **Problem Statement**
The password for the next level is stored in **/etc/bandit_pass/bandit14 and can only be read by user bandit14**. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level.

Until now, we have only logged into the remote machine using `ssh` with a password. An alternative to a password is using public-key cryptography. The public key is placed on the computers that should allow access (the remote host) to the user that owns the private key. Like with the password, it is important that only the user knows/owns the private key. The `-i` flag allows login with the private key.

`scp` is a command that uses SSH to transfer data over the network. The syntax to get a file from a remote host looks like the following: `scp -P <port> <user>@<IP>:<remotefilepath> <localfilepath>`. To send a file to a remote host, the local file path needs to stand at the beginning.

An alternative to this method is starting a simple web server with python. This is useful when you do not have ssh access. On the machine where the file is you need to start the webserver with the following command: `python3 -m http.server` (best is to do it in the directory of the file). On the receiving machine you then just have to send an HTTP request: `wget http://<ip>:8000/<pathtofile>`

### **Task**:
- Access the password for `bandit14` stored in `/etc/bandit_pass/bandit14` using a private SSH key provided for `bandit13`.
  - **Server**: `bandit.labs.overthewire.org`  
  - **Port**: `2220`  
  - **Username**: `bandit13`  
  - **Password**: `FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn`


### **Challenge**:  
- The password for `bandit14` is only readable by `bandit14`.  
- You must use the private key (`sshkey.private`) to log in as `bandit14`.

---

## 🚀**Solution Approach**
1. **Locate the SSH Key**: Find `sshkey.private` in `bandit13`'s home directory.  
2. **Transfer the Key**: Use `scp` to securely copy the key to your local machine.  
3. **Fix Permissions**: Ensure the private key has strict permissions (`chmod 600`).  
4. **SSH Login**: Authenticate as `bandit14` using the key.

---


### **Code Example**  
### Step 1: Transfer the SSH Key to Your Machine  
```bash
# On your local machine (replace <local-path> with your desired directory)
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private <local-path>
```

### Step 2: Secure the Key's Permissions
```bash
chmod 600 sshkey.private  # Restrict access to owner only
```

### Step 3: Log into bandit14 Using the Key
```bash
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

### Step 4: Retrieve the Password
```bash
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
MU4VWeTyJk8ROof199mcBPaLh7lDCPvS
```

So we got the next password🎉.

[https://overthewire.org/wargames/bandit/bandit13.html](https://overthewire.org/wargames/bandit/bandit13.html)

---

## Key Takeaways

- **HSSH Key Authentication:**
  - Private keys (`-i` flag) allow passwordless login.
  - Always set strict permissions (`600`) on private keys to prevent security warnings.

- **`scp` Command:**
  - Securely transfer files between local and remote machines over SSH.

- **File Permissions:**
  - Use `chmod 600 <key>` to restrict access to the owner (read/write only).
 
  
## References
- [OverTheWire Bandit Level 13](https://overthewire.org/wargames/bandit/bandit13.html)
- [Linux `scp` Guide](https://linux.die.net/man/1/scp)
- [SSH Key Permissions](https://superuser.com/questions/215504/permissions-on-private-key-in-ssh-folder/215506#215506)


 ## Additional Notes
 - **Alternative Transfer Methods:**
    - Use a Python HTTP server:

```bash
# On the remote server (bandit13)
python3 -m http.server 8000
# On your local machine
wget http://bandit.labs.overthewire.org:8000/sshkey.private
```

- **Troubleshooting:**
  - Error `Permissions too open`? Run `chmod 600 sshkey.private`.
  - Use `ssh -v` for verbose debugging if authentication fails.

Next Level: [Bandit Level 14 → 15](https://github.com/deejonsen/OverTheWire-Bandit-Games/blob/main/Bandit_Level_14.md)

---



![Screenshot 2025-04-14 174151](https://github.com/user-attachments/assets/556e622f-ed8e-44b8-b368-1fd6085f5a3e)
![Screenshot 2025-04-14 174243](https://github.com/user-attachments/assets/9cda5973-f0bd-48b7-b22f-ec50ab4ba11b)
![Screenshot 2025-04-14 174743](https://github.com/user-attachments/assets/2af3af19-9dc4-48e9-8390-b6c84f0ece9f)
![Screenshot 2025-04-14 174819](https://github.com/user-attachments/assets/474b8ae5-88cf-4e8c-818a-dfd2f5e6b655)
![Screenshot 2025-04-14 174835](https://github.com/user-attachments/assets/a529e191-0f69-4244-a760-3db3785f170e)
![Screenshot 2025-04-14 175049](https://github.com/user-attachments/assets/4b0aedb4-02a8-4c6b-95f2-559944732ba6)
