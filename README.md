
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


# 📌 MySQL Cheat Sheet

A quick reference guide for MySQL commands and queries. 🚀

## 📌 Basics
```sql
-- Login to MySQL
mysql -u username -p

-- Show databases
SHOW DATABASES;

-- Select a database
USE database_name;

-- Show tables in a database
SHOW TABLES;

-- Describe table structure
DESCRIBE table_name;

-- Create a new database
CREATE DATABASE database_name;

-- Drop a database
DROP DATABASE database_name;
```

## 📌 Table Management
```sql
-- Create a table
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Drop a table
DROP TABLE table_name;

-- Rename a table
RENAME TABLE old_table_name TO new_table_name;

-- Truncate a table (delete all rows, keep structure)
TRUNCATE TABLE table_name;
```

## 📌 Data Manipulation
```sql
-- Insert data
INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com');

-- Update data
UPDATE users SET name = 'Jane Doe' WHERE id = 1;

-- Delete data
DELETE FROM users WHERE id = 1;
```

## 📌 Querying Data
```sql
-- Select all columns
SELECT * FROM users;

-- Select specific columns
SELECT name, email FROM users;

-- Filtering results
SELECT * FROM users WHERE email = 'john@example.com';

-- Sorting results
SELECT * FROM users ORDER BY name ASC;

-- Limit results
SELECT * FROM users LIMIT 5;

-- Count rows
SELECT COUNT(*) FROM users;
```

## 📌 Joins
```sql
-- Inner Join
SELECT users.name, orders.amount 
FROM users 
INNER JOIN orders ON users.id = orders.user_id;

-- Left Join
SELECT users.name, orders.amount 
FROM users 
LEFT JOIN orders ON users.id = orders.user_id;
```

## 📌 Indexes
```sql
-- Create an index
CREATE INDEX idx_email ON users(email);

-- Show indexes
SHOW INDEXES FROM users;

-- Drop an index
DROP INDEX idx_email ON users;
```

## 📌 Transactions
```sql
-- Start a transaction
START TRANSACTION;

-- Rollback a transaction
ROLLBACK;

-- Commit a transaction
COMMIT;
```

## 📌 Users & Permissions
```sql
-- Create a new user
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';

-- Grant privileges
GRANT ALL PRIVILEGES ON database_name.* TO 'newuser'@'localhost';

-- Show user privileges
SHOW GRANTS FOR 'newuser'@'localhost';

-- Remove user
DROP USER 'newuser'@'localhost';
```

## 📌 Backup & Restore
```sql
-- Backup database
mysqldump -u username -p database_name > backup.sql

-- Restore database
mysql -u username -p database_name < backup.sql
```

### 🚀 Happy Querying! 🎯


