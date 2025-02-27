#!/bin/bash

# Step 1: Install Apache Server
echo "Installing Apache server..."
sudo apt update && sudo apt install -y apache2

# Step 2: Remove the Default Index File
echo "Removing default index file..."
sudo rm /var/www/html/index.html

# Step 3: Create an .htaccess File for Redirection
echo "Setting up .htaccess for redirection..."
echo "RedirectMatch 301 ^/$ /admin/" | sudo tee /var/www/html/.htaccess

# Step 4: Enable .htaccess in Apache Configuration
echo "Updating Apache configuration to allow .htaccess overrides..."
sudo sed -i 's/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf

# Step 5: Restart Apache to Apply Changes
echo "Restarting Apache service..."
sudo service apache2 restart

# Step 6: Deploy Fake Admin Login Page
echo "Deploying fake admin login page..."
echo '<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Panel</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            text-align: center;
            padding: 50px;
        }
        .login-container {
            background: white;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            display: inline-block;
            border-radius: 10px;
        }
        input {
            display: block;
            margin: 10px auto;
            padding: 10px;
            width: 80%;
        }
        button {
            background-color: #007bff;
            color: white;
            padding: 10px 20px;
            border: none;
            cursor: pointer;
            width: 80%;
        }
        .error {
            color: red;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h2>Admin Login</h2>
    <div class="login-container">
        <input type="text" id="username" placeholder="Username">
        <input type="password" id="password" placeholder="Password">
        <button onclick="validateLogin()">Login</button>
        <p class="error" id="error"></p>
    </div>
    <script>
        function validateLogin() {
            let user = document.getElementById('username').value;
            let pass = document.getElementById('password').value;
            if (user === "admin" && pass === "password123") {
                window.location.href = "dashboard.html";
            } else {
                document.getElementById('error').innerText = "Invalid credentials. Try again.";
            }
        }
        console.log("Nice try! But this is a rabbit hole.");
    </script>
</body>
</html>' | sudo tee /var/www/html/admin/index.html

echo "Apache setup completed with fake login page as a rabbit hole!"
