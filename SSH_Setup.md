#!/bin/bash

# Step 1: Set an Easy Password for SSH User
echo "Setting a weak password for SSH user..."
echo "majorsreekumar69:password123" | sudo chpasswd

# Ensure SSH server is installed
echo "Installing OpenSSH server if not already installed..."
sudo apt update && sudo apt install -y openssh-server

# Enable and start SSH service
echo "Enabling and starting SSH service..."
sudo systemctl enable ssh
sudo systemctl start ssh

# Check SSH service status
echo "Checking SSH service status..."
sudo systemctl status ssh --no-pager

# Step 2: Ensure SSH Allows Password Logins
echo "Configuring SSH to allow password authentication..."
sudo sed -i 's/^#PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
sudo sed -i 's/^#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# Restart SSH to apply changes
echo "Restarting SSH service..."
sudo systemctl restart ssh

echo "SSH setup completed with weak credentials!"
