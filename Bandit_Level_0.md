---
# OverTheWire Bandit Level 0 Walkthrough

---

## **Overview**  
This report documents the solution and key learnings for **OverTheWire Bandit Level 0**, a beginner-friendly challenge focused on establishing an SSH connection to a remote server. This level wants you to use SSH, which is short for Secure Shell Protocol. It is used to remotely connect to a machine. As the name suggests, this protocol aims for secure communication between the machines.

When you work with Linux, you can ssh into a machine through a terminal using the ssh command. Like with almost any Linux command, if you want to know more about it and its options, you can use the man command (man ssh).

With Windows, you can use software like PuTTY.

It is a very common service. So common in fact that it was assigned its own standard port, Port 22. A port is an endpoint that allows your computer to know which service should be accessed - kind of like office room numbers, so you know in which room the person you need to talk to is.

You can find a lot more information about these concepts on the internet. If you are not at all familiar with these, I would recommend you to watch an introduction to networking you can find to get a better overview of these and some more essential concepts.
 


---

## **Problem Statement**

- ### **Task**: Connect to the OverTheWire Bandit server via SSH.  
  - **Server**: [bandit.labs.overthewire.org](bandit.labs.overthewire.org) 
  - **Port**: `2220`  
  - **Username**: `bandit0`  
  - **Password**: `bandit0`  

---

## 🚀**Solution Approach**
The goal is to use the `ssh` command to authenticate and log into the server.  
1. **Command Structure**: The SSH command requires specifying the username, server address, and port.  
2. **Authentication**: Enter the password when prompted (input is hidden for security).  
3. **Confirmation**: A success message appears upon successful login.  


To ssh into the machine, I used a Linux terminal. The basic command structure of the ssh command that we need to look at for this level is the following:

ssh bandit0@bandit.labs.overthewire.org -p 2220

Running the command, you should then be prompted for the password, which you can just type in (under Linux the password is not displayed when you type it).

bandit0@bandit.labs.overthewire.org's password:

If you typed in the correct password, you should now be logged into the remote machine and see a Welcome text with more information about the game.

Since the task was only to log in, this concludes level 0.

---

### **Code Example**  
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```
### **Output**
```bash
bandit0@bandit.labs.overthewire.org's password: [hidden input]
Welcome to OverTheWire!
```

---

![Screenshot 2025-04-13 193700](https://github.com/user-attachments/assets/c0ae8b25-dedd-4c4c-bec4-8bec5df000ac)
![Screenshot 2025-04-13 193623](https://github.com/user-attachments/assets/24025232-ded1-4f82-9970-417eec7bc689)
![Screenshot 2025-04-13 193546](https://github.com/user-attachments/assets/6d9eabd6-5bab-4374-b83d-f4273cdab4d7)
![Screenshot 2025-04-13 193425](https://github.com/user-attachments/assets/be3db7cc-8096-4467-840a-cc1d94ed3646)
