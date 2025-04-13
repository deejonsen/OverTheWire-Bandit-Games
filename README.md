---

# OverTheWire: Bandit Walkthrough

---

This is a step-by-step guide and solutions for the [Bandit](https://overthewire.org/wargames/bandit/) wargame by OverTheWire. This repository provides detailed explanations and commands to help you progress through each level while understanding core cybersecurity and Linux concepts.


## **Description**
OverTheWire’s Bandit is a beginner-friendly Capture The Flag (CTF) game designed to teach Linux commands, file systems, and basic security concepts. Each level requires you to find a password to advance to the next level, often by exploiting common vulnerabilities or using command-line tools.

This repository contains:
- **Solutions** for all Bandit levels (0–15).
- **Detailed explanations** of the commands and techniques used.
- **Tips** to reinforce learning and troubleshooting.

## **Prerequisites**
- Basic familiarity with the Linux command line.
- An SSH client (e.g., OpenSSH on Linux/macOS, PuTTY on Windows).
- An internet connection to connect to the OverTheWire server.

## **Getting Started**
1. **Clone the repository:**
   ```bash
   git clone https://github.com/deejonsen/OverTheWire-Bandit-Games.git
   ```
   
 2. **Connect to the Bandit server:**
    ```bash
    ssh bandit0@bandit.labs.overthewire.org -p 2220
    ```
    - Password: `bandit0` (for the initial level).

  ---

## **Repository Structure**
Each level has its own directory (e.g., level-0-1 for Level 0 → Level 1).

### Solutions include:

- Step-by-step guide and commands.
- Key concepts and additional context.

### **Walkthroughs**
 Level        | Topic                                                             | Solution Links                |
|-------------|-------------------------------------------------------------------|-------------------------------|
| 0 → 1       |	SSH, file navigation	                                            | Level 0 Solution              |
| 1 → 2	      | File reading	                                                    | Level 1 Solution              |
| 2 → 3       |                                                                   |                               |
| 3 → 4       |                                                                   |                               |
| 4 → 5       |                                                                   |                               |
| 5 → 6       |                                                                   |                               |
| 6 → 7       |                                                                   |                               |
| 7 → 8       |                                                                   |                               |
| 8 → 9       |                                                                   |                               | 
| 9 → 10      |                                                                   |                               |
| 10 → 11     |                                                                   |                               |  
| 11 → 12     |                                                                   |                               |
| 12 → 13     |                                                                   |                               |
| 13 → 14     |                                                                   |                               |
| 14 → 15     |                                                                   |                               |
| 15 → 16     |                                                                   |                               |


---


## **Key Takeaways**

### SSH Basics:
- SSH (Secure Shell) is used for secure remote access to servers.
- Default SSH port is `22`, but custom ports (e.g., `2220`) are often used for security.

### Command-Line Tools:
- **Linux/macOS:** Use the native `ssh` command.
- **Windows:** Tools like PuTTY or Windows Subsystem for Linux (WSL) are required.
- **Documentation:** Use `man ssh` to explore SSH options and flags.


### **Contribute:**
Contributions are welcome! If you have:
  - Alternative solutions or optimizations.
  - Corrections for errors or typos.
  - Additional explanations or tips.

**Please:**

  - Fork the repository.
  - Create a branch for your changes.
  - Submit a pull request with a clear description.


### **Acknowledgments**
  - [OverTheWire](https://overthewire.org/) for creating the Bandit game.
  - [SSH Documentation](https://www.openssh.com/manual.html)
  - The cybersecurity community for fostering collaborative learning.


## **Important Notes**
- **Ethical Use:** This guide is for educational purposes only. Use your skills responsibly.
- **Do Not Copy-Paste:** Understand the commands instead of blindly running them.
- **Join the Community:** Struggling? Ask for help on the [OverTheWire Forum](https://forum.overthewire.org/).


### **Additional Notes**
- **Password Security:** Passwords are not displayed when typed in Linux terminals.
- **Troubleshooting:**
  - Ensure the SSH client is installed (e.g., `openssh-client` on Debian-based systems).
  - Verify network connectivity if the connection fails.


Happy Hacking! 🚀

---
