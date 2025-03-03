# CTF Vulnerable Machine - Hard Linux Challenge

## Overview
Welcome to the **Hard Linux CTF Machine**, a custom-built vulnerable machine designed for penetration testers and CTF enthusiasts! This machine features multiple attack vectors and requires a combination of enumeration, exploitation, and privilege escalation techniques to gain root access.

## Features
- **Target OS:** Linux 14
- **Attack Vectors:**
  - FTP Misconfigurations
  - SSH Exploits
  - Brute Force Attacks
  - Hidden Hints in Audio Morse Code
  - Steganography Challenges
- **Flags:**
  - `user.txt` - Obtainable via SSH
  - `root.txt` - Accessible only through a cron job exploit

## Download & Setup
Due to GitHub's file size limitations, download the virtual machine from the link below:

🔗 **[Download the VM - Google Drive](https://drive.google.com/file/d/1GZzrimgIg6WFpvEwdWVzxBtZeqnBqLru/view?usp=drive_link)**

### Importing the VM
1. Download the `.ova` file from the above link.
2. Open VirtualBox or VMware.
3. Import the `.ova` file and configure network settings as needed.
4. Start the machine and begin your attack!

## Walkthrough (Spoiler-Free)
- **Enumeration**: Identify open services (FTP, SSH, Web) and analyze vulnerabilities.
- **Initial Foothold**: Find the weak credentials or exploit misconfigurations.
- **Privilege Escalation**: Analyze cron jobs, file permissions, and hidden scripts to escalate privileges.
- **Capture the Flags**: Retrieve `user.txt` and `root.txt`.

## Hints
- Check FTP for interesting files.
- Look at hidden messages in images.
- Listen carefully to the audio files.
- Inspect scheduled tasks (`cronjobs`).

## Writeups & Solutions
If you've completed this machine, feel free to submit a write-up or share your methodology!

## License
This project is released under the [MIT License](LICENSE).

---

Happy hacking! 🚀

