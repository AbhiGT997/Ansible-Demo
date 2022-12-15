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


