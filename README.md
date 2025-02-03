
# MySQL Installation Guide for Ubuntu

MySQL is a popular open-source relational database management system. This guide will walk you through the installation and basic configuration of MySQL on Ubuntu.

## Prerequisites
- A system running Ubuntu (20.04, 22.04, or later).
- A user with **sudo** privileges.

## Step 1: Update System Packages
Before installing MySQL, update your system's package list to ensure you get the latest version:

```bash
sudo apt update && sudo apt upgrade -y
```

## Step 2: Install MySQL Server
To install MySQL, run:

```bash
sudo apt install mysql-server -y
```

## Step 3: Secure MySQL Installation
MySQL includes a security script to remove insecure defaults. Run:

```bash
sudo mysql_secure_installation
```

### Recommended Security Settings:
- Set a **root password** (if not already set).
- Remove **anonymous users**.
- Disallow **remote root login**.
- Remove the **test database**.
- Reload **privilege tables**.

Answer **Yes (Y)** to all prompts for better security.

## Step 4: Verify MySQL Status
To check if MySQL is running:

```bash
sudo systemctl status mysql
```

If it's not running, start MySQL with:

```bash
sudo systemctl start mysql
```

To enable MySQL to start on boot:

```bash
sudo systemctl enable mysql
```

## Step 5: Log into MySQL
To access the MySQL shell:

```bash
sudo mysql -u root -p
```

Enter the **root password** when prompted.

## Step 6: Create a Database and User (Optional)
To create a new database and user, run the following commands inside MySQL:

```sql
CREATE DATABASE mydatabase;
CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypassword';
GRANT ALL PRIVILEGES ON mydatabase.* TO 'myuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

## Step 7: Allow Remote Connections (Optional)
If you need to allow remote connections:

1. Edit MySQL configuration:
   ```bash
   sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
   ```
2. Find the line:
   ```
   bind-address = 127.0.0.1
   ```
   Change it to:
   ```
   bind-address = 0.0.0.0
   ```
3. Restart MySQL:
   ```bash
   sudo systemctl restart mysql
   ```

## Step 8: Check MySQL Version
To verify the installed MySQL version:

```bash
mysql --version
```

## SQL Cheat Sheet
### Basic SQL Commands
```sql
-- Create a new database
CREATE DATABASE mydatabase;

-- Show all databases
SHOW DATABASES;

-- Use a specific database
USE mydatabase;

-- Create a new table
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Insert data into a table
INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');

-- Select data from a table
SELECT * FROM users;

-- Update data in a table
UPDATE users SET email = 'alice@newdomain.com' WHERE name = 'Alice';

-- Delete data from a table
DELETE FROM users WHERE name = 'Alice';

-- Drop a table
DROP TABLE users;

-- Drop a database
DROP DATABASE mydatabase;
```

## Conclusion
You have successfully installed and configured MySQL on Ubuntu. You can now start creating databases and managing your data.

For more details, visit the [official MySQL documentation](https://dev.mysql.com/doc/). 🚀



