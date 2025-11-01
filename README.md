# Ansible-Notes
## 🧩 What is Ansible..?
### Ansible is an open-source automation tool used for configuration management, application deployment, and infrastructure orchestration.
### It is created by Red Hat and is widely used in DevOps for managing servers automatically — without manually logging into each one.

## 💡 Simple Definition:
### Ansible helps you automate IT tasks — like installing software, managing configurations, and deploying applications — across many servers at once.

## ⚙️ Why Use Ansible...?
### Main Features In Ansible
* Agentless >>>>>>>	No agent needed on target systems (uses SSH)
* Simple YAML Syntax >>>>>>>	Uses easy-to-read files called Playbooks
* Idempotent >>>>>>>	Runs multiple times without changing existing state
* Cross-Platform	>>>>>>> Works with Linux, Windows, Cloud, etc.
* Integration	>>>>>>> Works with AWS, Docker, Kubernetes, Jenkins, etc.

## 🧱 Ansible Architecture
### Components Of Architechture
* Control Node (Master) >>>>>>>	Where Ansible is installed and commands are executed
* Managed Nodes (Clients) >>>>>>>	Servers or systems that Ansible manages
* Inventory File	>>>>>>> A file that lists all target hosts
* Modules >>>>>>>	Reusable scripts for performing tasks (e.g., install packages)
* Playbook	>>>>>>> A YAML file that defines what tasks to run
* Task	>>>>>>> A single action (e.g., install nginx) inside a playbook

## 🧰 Basic Ansible Commands:
### 🔹 1. Check Ansible Version
* ansible --version

## 🔹 2. Check Connectivity (Ping Test)
### 👉 Tests connection to all hosts listed in the inventory file.
* ansible all -m ping

## 🔹 3. Run a Simple Command
### 👉 Runs a shell command on all or specific hosts.
* ansible all -a "uptime"
* ansible webservers -a "df -h"

## 🔹 4. Specify Inventory File
* ansible -i inventory.ini all -m ping

## 🔹 Example inventory.ini:
* [webservers]
* server1 ansible_host=192.168.1.10
* server2 ansible_host=192.168.1.11

## 🔹 5. Run an Ad-Hoc Command with Module
* ansible all -m yum -a "name=httpd state=present"    👉 For RHEL/CentOS
* ansible all -m apt -a "name=nginx state=latest"     👉 For Ubuntu/Debian

## 🔹 6. Run a Playbook
* ansible-playbook playbook.yml

## 🔹 7. Check Syntax of Playbook
* ansible-playbook playbook.yml --syntax-check

## 🔹 8. Run Playbook in Check (Dry Run) Mode
* ansible-playbook playbook.yml --check

## 🔹 9. View Inventory
* ansible-inventory --list -y

## 🔹 10. Gather System Facts
* 👉 Collects detailed info about managed nodes (CPU, memory, etc.)
* ansible all -m setup

## 🧾 Example Playbook
### playbook.yml
* ---
* - name: Install and start Nginx
  * hosts: webservers
  * become: yes
  * tasks:
    * - name: Install Nginx
      * apt:
        * name: nginx
        * state: present
        * update_cache: yes

    * - name: Start Nginx service
      * service:
        * name: nginx
        * state: started
        * enabled: yes

## ⚙️ Typical Ansible Workflow
### 👉 Install Ansible on control node
### 👉 Create an inventory file (/etc/ansible/hosts)
### 👉 Write a playbook (.yml)
### 👉 Run the playbook using ansible-playbook
### 👉 Verify changes on target servers
