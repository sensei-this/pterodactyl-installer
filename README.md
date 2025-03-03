# Pterodactyl Installer 🦖

Welcome to the **Pterodactyl Installer** repository! 🎉 This installer is designed to help you easily install and set up the Pterodactyl Panel on **Debian-based** or **RHEL-based** machines. If you encounter any issues during the installation process, please refer to our troubleshooting section for helpful tips. 🛠️

## Installation 📝

Follow these steps to get started:

1. 🧹 **Prepare your machine**: Ensure that your machine is freshly reinstalled if you've made any changes to it beforehand. A clean setup will help avoid conflicts during installation.

2. 🌐 **DNS Configuration**: Point a **DNS A-Record** to your machine's IP address. For example, you can point `panel.example.com` to `0.0.0.0`.

3. 📥 **Download and Run the Installer**: To download and run the installer, simply enter the following command into your terminal and follow the prompts:
```
bash <(curl -Ss https://raw.githubusercontent.com/sensei-this/pterodactyl-installer/main/install.sh || wget -O - https://raw.githubusercontent.com/sensei-this/pterodactyl-installer/main/install.sh) auto
```

# 📌 Database Installation on Pterodactyl

## 1️⃣ Preparing the Server

🔹 Make sure you have **Pterodactyl Panel** and **Wings** installed.  
🔹 Install **MySQL** or **MariaDB** on the panel server.  
🔹 Check if port **3306** (or another if using a custom one) is open.  

---

## 2️⃣ Configuring Database Access

🔹 Open the database configuration file:  
```bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```

🔹 Find the following line:
```ini
bind-address = 0.0.0.0
```
Replace `0.0.0.0` with your IP address (e.g., `192.168.1.100`).  

🔹 Save the changes (Ctrl + X → Y → Enter).  

🔹 Restart MySQL/MariaDB:  
```bash
sudo systemctl restart mysql
sudo systemctl restart mariadb
```

🔹 Open MySQL:  
```bash
mysql -u root -p
```

🔹 Select the MySQL database:  
```sql
USE mysql;
```

🔹 Create a new user:  
```sql
CREATE USER 'username'@'%' IDENTIFIED BY 'password';
```

🔹 Grant all privileges:  
```sql
GRANT ALL PRIVILEGES ON *.* TO 'username'@'%' WITH GRANT OPTION;
```

🔹 Flush privileges:  
```sql
FLUSH PRIVILEGES;
```

🔹 Exit MySQL:  
```sql
EXIT;
```

---

## 3️⃣ Creating a Database in the Panel

1. Log into Pterodactyl Panel as an **administrator**.  
2. Go to **Admin Panel** → **Databases**.  
3. Click **Create Database**.  
4. Specify:  
   - **Database Name**  
   - **Server to link the database to**  
   - **Database Host** (your IP or `127.0.0.1` if local)  
5. Save the changes.  

---

## ✅ Done!

Your database is now set up and ready to use! 🚀

## Post Installation 🛠️

* Please note that "example.com" refers to the **panel URL** you set during the installation process. 🌐

1) After the installation is complete, go to [http://example.com/admin/nodes/view/1/allocation](http://example.com/admin/nodes/view/1/allocation) to add the necessary ports for your games. 🎮

## Troubleshooting ⚠️

1) If you receive a **MySQL connection error** 💻, you may have run the installer multiple times. In this case, the best solution is to **reinstall your operating system** and run the install script again. 🔄

2) If you encounter **Let's Encrypt SSL generation errors** 🔒, it could be because you're using an **IP address** instead of a domain, or because the **FQDN** you're trying to generate an SSL for doesn't have an **A-Record** pointing to your machine IP. 🌍


## Compatible Operating Systems:
| Operating System | Version | Supported          | PHP Version |
| ---------------- | ------- | ------------------ | ----------- |
| Ubuntu           | 20.04   | :white_check_mark: | 8.3         |
|                  | 22.04   | :white_check_mark: | 8.3         |
|                  | 24.04   | :white_check_mark: | 8.3         |
| Debian           | 11      | :white_check_mark: | 8.3         |
|                  | 12      | :white_check_mark: | 8.3         |
|                  | 13      | :red_circle: \*    |             |
| Rocky Linux      | 8       | :white_check_mark: | 8.3         |
|                  | 9       | :white_check_mark: | 8.3         |
| AlmaLinux        | 8       | :white_check_mark: | 8.3         |
|                  | 9       | :white_check_mark: | 8.3         |
