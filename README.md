 # **Installation and configuration of a web server using Ansible**

We will be running this project on AWS using an EC2 instance.
- First of all setup an EC2 instance machine on AWS and after that install Ansible to get started with the project. The commands to install Ansible are provided below.

### Ansible Installation Steps  

```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```


## **# Setup**

To get this repository, run the following command inside your git-enabled terminal
```bash
git clone https://github.com/AsifAnsari360/ansible-proj.git
```

Once you have installed Ansible. Use the ssh method to authenticate the controller node to be able to connect to the Target Node.
```bash
sudo vim /etc/ansible/hosts
```
In the hosts file add the below lines of code. Add your instance's Public IP address. 
```bash
[servers]
ansible-server ansible_host=<Public IP>
```
Create a keys directory on your remote terminal, to copy the your_key_name.pem key from the local system to your remote instance (keys directory). Open the terminal on your local system and change the directory where you have saved your security key (your_key_name.pem). 

- In your Remote terminal 
```bash
mkdir keys
cd keys
```
- First, change the user permissions of your your_key_name.pem file using the below command. [In local terminal] 
```bash
chmod 400 test-key.pem
```
- To copy your_key_name.pem from local to remote use the below command. [In local terminal ]
```bash
 scp -i "test-key.pem" test-key.pem ubuntu@ec2-13-201-74-249.ap-south-1.compute.amazonaws.com:/home/ubuntu/keys
```
The above scp command may be different for you. You can find it here.


After this again edit hosts, and add the following code for the controller node to be able to connect to the Target Node.
```bash
sudo vim /etc/ansible/hosts
```
```bash
[all:vars]
ansible_python_interpreter=/usr/bin/python3
ansible_user=ubuntu
ansible_ssh_private_key_file=/home/ubuntu/keys/test-key.pem  #your path may be different
```

- To check if the controller node is connected to the Target Node. Use the following command.
```bash
ansible servers -m ping
```

### Create an Index.html file in playbooks

- First, change your directory to
```bash
 cd /etc/ansible/
```
- Then create a playbook directory
```bash
 mkdir playbooks
```
- Change the directory to playbooks and in that create an index.html file.
```bash
 cd /playbooks
```
```bash
 sudo vim index.html
```
- Paste the HTML code in the index.html file.
```bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello, World!</title>
</head>
<body>
    <h1>Hello, World!</h1>
    <p>This is a simple HTML page.</p>
</body>
</html>
```

#### Come to the root directory where ansible.yml file is stored and RUN the following command.

- Once the playbook file is ready, we will check for the syntax of the playbook using the below command:
```bash
ansible-playbook --syntax-check ansible.yml
```
- Once the syntax is checked and is correct, we can proceed with running the playbook using the below command:
```bash
ansible-playbook ansible.yml
```

You can see your HTML web page using your Public IP Address. Copy your Public IP Address and Paste it on any web browser. 

Hence, we were successful in installing and configuring the Nginx server on Ubuntu via Ansible.




