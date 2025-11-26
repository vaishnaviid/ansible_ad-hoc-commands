# 📘 Ansible Ad-Hoc Commands Guide

## 🚀 Overview
This document is a complete reference of **Ansible ad-hoc commands** used for quick, one-line automation without writing a playbook.  
These commands help with testing, troubleshooting, and performing small tasks on remote servers.

---

## 📌 What Are Ad-Hoc Commands?

Ad-hoc commands are single-line Ansible operations executed using:
``` bash
ansible <host-group> -m <module> -a "<arguments>"
```
Example:
```bash
ansible webserver -m ping
```

# 🟦 1. Connectivity & Testing

### ✔ Ping all hosts
``` bash
ansible all -m ping
```
---
# 🟦 2. Running Shell Commands

### ✔ Check uptime
``` bash
ansible all -m shell -a "uptime"
```
### ✔ Disk usage
``` bash
ansible all -m shell -a "df -h"
```
### ✔ RAM usage
``` bash
ansible all -m shell -a "free -m"
```
---

# 🟦 3. Package Management

### ✔ Install package (Amazon Linux / RHEL / CentOS)
``` bash
ansible webserver -m yum -a "name=nginx state=present"
```
### ✔ Remove package
``` bash
ansible all -m yum -a "name=nginx state=absent"
```
### ✔ Install package (Ubuntu / Debian)
``` bash
ansible webserver -m apt -a "name=nginx state=present update_cache=yes"
```
---

# 🟦 4. Service Management

### ✔ Start service
``` bash
ansible webserver -m systemd -a "name=nginx state=started"
```
### ✔ Restart service
``` bash
ansible webserver -m systemd -a "name=nginx state=restarted"
```
### ✔ Enable service on boot
``` bash
ansible webserver -m systemd -a "name=nginx enabled=yes"
```
### ✔ Stop service
``` bash
ansible webserver -m systemd -a "name=nginx state=stopped"
```
---

# 🟦 5. File & Directory Management

### ✔ Copy a file to a remote server
``` bash
ansible webserver -m copy -a "src=index.html dest=/usr/share/nginx/html/index.html"
```
### ✔ Create a directory
``` bash
ansible all -m file -a "path=/opt/demo state=directory mode=0755"
```

### ✔ Delete a file or directory
``` bash
ansible all -m file -a "path=/tmp/oldfile.txt state=absent"
```
---

# 🟦 6. User Management

### ✔ Create user
``` bash
ansible all -m user -a "name=devops state=present"
```
### ✔ Delete user
``` bash
ansible all -m user -a "name=devops state=absent"
```
---

# 🟦 7. Fetch Files From Remote Server
``` bash
ansible webserver -m fetch -a "src=/etc/hosts dest=./backup/"
```
This downloads the file to your local machine.
---

# 🟦 8. Reboot Remote Hosts
``` bash
ansible all -m reboot
```
---

# 🟦 9. Gather System Information

### ✔ Full system facts
``` bash
ansible all -m setup
```
### ✔ Filter specific facts
``` bash
ansible all -m setup -a "filter=ansible_distribution"
ansible all -m setup -a "filter=ansible_mem*"
```
---

# 🟧 Common Useful Options

### ✔ Run commands using sudo
``` bash
ansible all -b -m shell -a "whoami"
```

### ✔ Use a specific inventory file
``` bash
ansible all -i inventory.ini -m ping
```

### ✔ Increase verbosity
``` bash
ansible all -m ping -vvv
```
---

# 📝 Example Inventory File (inventory.ini)
``` bash
[webserver]
172.31.10.5 ansible_user=ec2-user ansible_ssh_private_key_file=/home/ec2-user/key.pem

[db]
172.31.11.8 ansible_user=ec2-user ansible_ssh_private_key_file=/home/ec2-user/key.pem
```
---

# 🎯 Practice Tasks

1. Install nginx using ad-hoc commands  
2. Create a new user  
3. Copy a file to `/tmp`  
4. Fetch `/etc/hosts` file  
5. Restart nginx  
6. Check memory, CPU, and disk usage  

---

# ✅ Conclusion  
Ad-hoc commands are powerful for quick automation, debugging, and server management.  
Use this as a reference guide while practicing Ansible.
