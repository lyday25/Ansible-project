sudo apt update -y

ifconfig

sudo apt install net-tools

ifconfig

## ANSIBLE CONTROLLER
172.31.38.93
-----------------------
## TARGET MACHINE1
172.31.44.246
-----------------------
## TARGET MACHINE2
172.31.45.58
------------------------
## install ansible on the ansible controller by running this script
#!/bin/bash

#This is the script to install the ansible

sudo apt update -y

sudo apt-add-repository ppa:ansible/ansible -y

sudo apt update -y 

sudo apt install ansible -y

#confirm installation

ansible --version

## TO generate ssh key (Public & private key)
ssh-keygen
cd .ssh
ls
## cat the keys and note the public key, you will drop the pub in other target machines. Then go to target machine1
cd .ssh
ls
## copy authorised_key and vi. Then copy the ansible controller public key under it and save
## You can now ssh to the machines and type exit to go back to your ansible
ssh 172.31.44.246
ssh 172.31.45.58
## go back one step cd ..
touch inventory
vi inventory
open square bracket and type webservers and lineup the target machines

## To ping all target machines

ansible -i inventory all -m ping
ansible -i inventory webservers -m ping
## check for the list of items on the target machines
ansible -i inventory all -a "ls"
ansible -i inventory webservers -a "ls"
## check for the list of items and hidden files on the target machines
ansible -i inventory all -a "ls -lart"

# now make directory cloud on all machines
ansible -i inventory all -a "mkdir cloud"

# to create a file text.txt on all machines

ansible -i inventory all -a "touch cloud/text.txt"
## To remove cloud folder
ansible -i inventory all -a "rm -r -f cloud"

## adhoc commands

To put simply, Ansible ad hoc commands are one-liner Linux shell commands and playbooks are like a shell script, a collective of many commands with logic.

Ansible ad hoc commands come handy when you want to perform a quick task.

task

## To check the disk/memory space on all hosts in an inventory file

ansible -i inventory all -m shell -a 'df -h'

Or 

ansible -i inventory webservers -m shell -a 'df -h'

# ansible ad hoc command to check the free memory or memory usage of hosts

ansible -i inventory all -a "free -m"

# To find ids on host machines

ansible -i inventory webservers -m shell -a 'id'

# first create a file touch /tmp/my-file.txt on the control server and push it to all #machines

 touch /tmp/my-file.txt 

ansible -i inventory webservers -m copy -a "src=/tmp/my-file.txt dest=/tmp/my-file.txt"

# To copy a file to all hosts in an inventory file

ansible -i inventory -m copy -a 'src=/local/path/to/file dest=/remote/path/to/file mode=0644'

# You can check the status of a specific service on single hosts or server1

ansible -i inventory webservers -m service -a 'name=apache2 state=started'

# to install apache on all machines

ansible -i inventory webservers -m apt -a 'name=apache2 state=latest'

## Command could not run because, for multiple tasks you need to run a playbook
