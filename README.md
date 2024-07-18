Ansible ESXi Command Runner
This project provides an Ansible playbook to interact with an ESXi host by running various commands. The playbook retrieves a list of available commands from a GitHub repository and prompts the user to enter the ESXi credentials once. The user can then execute multiple commands without re-entering the credentials each time.

Prerequisites
Ansible installed on your local machine
Git installed on your local machine
Access to an ESXi host
A GitHub repository containing the command list (commands.yml)
Setup
Step 1: Create a GitHub Repository and Command List
Create a new GitHub repository (e.g., esxi-commands).
Add a file named commands.yml to the repository with the following content:

Step 2: Create Ansible Inventory File
Create or update the hosts.ini file with your ESXi host details:

Step 3: Create Ansible Playbook
Create or update the Ansible playbook run_nscli_with_prompt.yml:

Step 4: 
ansible-playbook -i hosts.ini run_nscli_with_prompt.yml
