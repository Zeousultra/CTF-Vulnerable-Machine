#!/bin/bash

# Step 1: Install vsftpd
echo "Installing vsftpd..."
sudo apt-get update
sudo apt-get install -y vsftpd

# Step 2: Configure vsftpd
echo "Configuring vsftpd..."
sudo bash -c 'cat > /etc/vsftpd.conf <<EOF
write_enable=YES
local_enable=YES
chroot_local_user=YES
allow_writeable_chroot=YES
EOF'

# Step 3: Restart vsftpd Service
echo "Restarting vsftpd service..."
sudo service vsftpd restart

# Step 4: Ensure the FTP Directory Exists
echo "Creating FTP directory..."
sudo mkdir -p /srv/ftp/

# Step 5: Set Proper Permissions for Anonymous Access
echo "Setting permissions..."
sudo chmod 755 /srv/ftp/
sudo chown nobody:nogroup /srv/ftp/

# Step 6: Place the Hint File Inside FTP Directory
echo "Creating hint file..."
echo "Find the next clue inside an image..." | sudo tee /srv/ftp/hint.txt

# Step 7: Restart vsftpd to Apply Changes
echo "Restarting vsftpd service again..."
sudo service vsftpd restart

echo "FTP setup completed successfully!"
