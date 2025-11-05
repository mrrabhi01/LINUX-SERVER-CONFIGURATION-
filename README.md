# Linux Server Setup (Apache + MySQL + FTP + UFW)

This guide provides all commands required to configure a Linux server with Firewall, Apache Web Server, MySQL Database Server, and VSFTPD FTP Server on Ubuntu/Debian systems.

---

## Setup Commands

```bash
# Update System
sudo apt update && sudo apt upgrade -y

# Firewall Configuration (UFW)
sudo apt install ufw -y
sudo ufw enable
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow 3306/tcp
sudo ufw allow ftp
sudo ufw status verbose
ip a

# Apache Web Server
sudo apt install apache2 -y
sudo systemctl status apache2
sudo systemctl enable apache2
sudo nano /var/www/html/index.html
sudo systemctl restart apache2
curl http://127.0.0.1

# MySQL Server
sudo apt install mysql-server -y
sudo mysql_secure_installation
sudo mysql -u root -p

# Inside MySQL:
# -------------------------
# CREATE DATABASE project_db;
# CREATE USER 'project_user'@'localhost' IDENTIFIED BY 'secure_password';
# GRANT ALL PRIVILEGES ON project_db.* TO 'project_user'@'localhost';
# FLUSH PRIVILEGES;
# -------------------------

# Test MySQL Login
mysql -u project_user -p

# VSFTPD FTP Server
sudo apt install vsftpd -y
sudo nano /etc/vsftpd.conf
sudo adduser ftp_user
sudo chown -R ftp_user:ftp_user /home/ftp_user
mkdir /home/ftp_user/ftp_files
sudo chmod a-w /home/ftp_user
sudo chown -R ftp_user:ftp_user /home/ftp_user/ftp_files
sudo systemctl restart vsftpd
sudo systemctl status vsftpd
