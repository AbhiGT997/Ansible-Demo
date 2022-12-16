# Ansible-Automation in AWS-EC2 Instances 
#Here is a small guide for setting up Asible in your AWS-EC2 instances and automating tasks to the worker nodes

#Getting Started with Ansible on AWS-EC2 Ubuntu distribution Packege
Create an EC2 Instance with Ubuntu image (default catlog) and log in to it.

#Get the system up to date
Run sudo apt install updates

#Pre-Requirements for Ansible
1. It requires an open ssh connection between the Master and the Node servers
2. Inventory file containing all the nodes ip addresses
3. An version-controll repo for committing the codes
4. ansible-playbook scripst for performing automation

#Configuring Master-System (Ubuntu distribution)

#Creating an open ssh connection:
Create an Secure shell connection between Master system and its Nodes servers
1. ssh-keygen -t ed25519 -C "Ansible-Master" [-t=typr ed25519 More secure, Short-key SSh, -C=comment]
2. Directory selection leave default.
3. Pass-phrase: give any (123,qwer,..etc)
4. A rsp public & private key files would be created in ~/.ssh/ 
5. Create a Worker Instance with same Distribution Packaqe "ubuntu" and install updates. 
6. Copy the contents of id_ed25519.pub from Ansible Master System to worker systems ssh directory ie ~/.ssh/authorized_keys (Insert after the ppk key, The whole content has to be inserted including the comment at the very end, id and the key it-self.
7. check if the connection works with ssh <IP address of the worker node> (it will ask for the pass-phrase give the earlier mentioned one)

#Create a ssh-key dedicated for ansible (To access the nodes automatically)
1. use ssh-keygen -t ed25519 -C "ansible" 
2. Change the default location because it would over-write the earlier data hence use /home/ubuntu/.ssh/ansible
3. "Do not" give a pass-phrase here, leave it blank.
4. ansible.pub (public key) would be generated, copy (use cat to display it and copy) all the contents to the authorized key of Worker node server (Server 2)

#Logging-in without using Pass-phrase

Use command eval $(ssh-agent) and ssh-add [The identity would be added and the ssh agent would use the saved pass-phrase to log in automatically]
but NOTE: it would be of temperory in nature and if the terminal is shut down it would be lost hence, to save it permanently we can create an Alias in Linux]
1. Create an Alisa and add to .bashrc file (Linux boot-up file) such that every time the session is booted up the ssh agent would be spun up.
2. Add alias ssha = 'eval $(ssh-agent) && ssh-add' [At the end of .bashrc file. Nano editor can be used for this nano .bashrc scroll down and paste the command)
3. Duplicate the the session to check if its working use ssha and it would ask for pss phrase once only then it would be saved permantely on the system.

#Ansible Installation
1. Use sudo apt install ansible (ubuntu default)
2. Check the version after installation ansible --version.
3. Install ansible on both Master system and all the worker nodes.
4. Create a directory mkdir ~/home/ubuntu/ansible cd into it.
5. Create a file called inventory and paste all the worker servers ip addresses and save the file.
6. Then we can ping to check if the servers are connected or not ansible all --key-file ~/.ssh/ansible -i inventory -m ping
7. Note: The IP addressed of AWS EC2 machines would be changing and the inventory file need to be updated with the new ip address if new session is selected.
8. To make the command shorter (to automate it) a ansile configuration file has to be added ie: nano ansible.cfg with the following contents
[defaults]
inventory = inventory
private_key_file = ~/.ssh/ansible
<save and exit>

Then you can run commands:
ansible all -m ping
ansible all --list-hosts
ansible all -m gather_facts



