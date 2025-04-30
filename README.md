# my-ec2-project
#!/bin/bash

# Update the package list
sudo apt update -y

# Install Apache2
sudo apt install apache2 -y

# Enable and start Apache2
sudo systemctl enable apache2
sudo systemctl start apache2

# Set up a basic HTML file
echo "<h1>Welcome to my Apache2 Web Server on EC2!</h1>" | sudo tee /var/www/html/index.html

# Allow Apache through the firewall (UFW only if it's active)
if sudo ufw status | grep -q active; then
  sudo ufw allow 'Apache'
  sudo ufw reload
fi

# Optional: Set permissions (if using a non-root user)
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html



