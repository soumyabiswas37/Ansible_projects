🌐 Ansible Playbook to deploy webpage in EC2 Instance with different AMI🌏

Introduction:
The requirement is to create configure webservices in in Machines which are configured with AWS Linux and Redhat Linux

Requirements:
- AWS Account
- Skill of Ansible to develop playbook

Tasks:
- Launch an EC2 instance as per requirement met in AWS Free tier account to setup the controller node and login to it with ec2-user.
- Install "ansible-core" in the machine:
Command: "sudo dnf install ansible-core -y"
-Check with below command to know the ansible version:
ansible --version
- Configure the ansible.cfg file in user's home directory with below command:
ansible-config init --disabled > ansible.cfg
- To verify if the same file is getting reflected as configuration file, user the below command:
ansible --version
- Change the below settings in ansible.cfg file:
host_key_checking=False

And below settings in Privilege_escalation section:
become=True
become_ask_pass=False
become_method=sudo
become_user=root

- Create a local hosts files and mention the file path in ansible.cfg file to consider the file as hosts file (in general, /
etc/ansible/hosts file is the default static inventory)

- Launch two more EC2 instance in AWS, one with RedHat and another one with AWS Linux.
- Login to the newly launched instances and create a sudo user to have permission to execute all command in sudo mode.
-In controller machine, go to locally created inventory or the default static inventory(in case local inventory is not created) and add the IP address of the managed nodes, username and password in below format and save it:
IPADDRESS/Alias ansible_user=user_name ansible_password=password
- After all this configuration, write the playbook as per the screenshot attached
- Check the syntax in case of any syntax error:
ansible-playbook --syntax-check playbook_name.yml
- In case of no error, execute it with below command:
ansible-playbook playbook_name.yml
- In runlog, some error might be observed. The errors occurred because there was no package named VLC to be installed in managed nodes.
