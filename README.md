# Ansible-jenkins
This is the ansible playbook to automatically setup jenkins server over docker in remote server.
## The steps for proceeding further are as follows :-
### STEP-1 Install ansible in your system
For installing ansible follow the below official documentation.
[Ansible Installation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
### STEP-2 Update the inventory file
If the server is an EC2 instance the we have to write the inventory file as follows-

```
[ec2]
<EC2 instance IP> ansible_ssh_user=<SSH username> ansible_connection=ssh  ansible_ssh_private_key_file=<EC2 instance private key path(.pem file)> ansible_python_interpreter=/usr/bin/python3
```
Replace the values of the following according to your instance details
1. EC2 instance IP
2. SSH username
3. EC2 instance private key path(.pem file)
### STEP-3 Running the Playbook
Clone the repository in your local system.
The directory structure after cloning will be as shown below
```
.
├── build_src
│   ├── default-user.groovy
│   ├── Dockerfile
│   └── plugins.txt
├── docker-compose.yml
├── docker.yml
├── jenkins_docker.retry
├── jenkins_docker.yml
├── jenkins.service
├── master.yml
└── README.md

1 directory, 10 files
```
## change the paths in files wherever required.
Now we have the customized dockerfile for customized jenkins server.
A docker-compose file for deploying jenkins server over docker.
A master.yml file which runs two playbooks 
1. docker.yml
2. jenkins_docker.yml

The `docker.yml` playbook setup docker and docker-compose into the remote server if not present.

The `jenkins_docker.yml` setup jenkins server over docker in remote server.

To run the playbooks
```
#ansible-playbook master.yml
```
To run the playbook with verbose 
```
#ansible-playbook master.yml -vv
```
#Increase or decrease the number of v for depth of verbosity you want.

## Output of the playbook should look something as shown below
![output1](https://github.com/AyushGupta88/Ansible-jenkins/blob/2cb93ab611037cda1aa4f76f3c0697a7d0c56b2e/Screenshot%20from%202021-09-28%2012-22-42.png "Logo Title Text 1")
![output2](https://github.com/AyushGupta88/Ansible-jenkins/blob/2cb93ab611037cda1aa4f76f3c0697a7d0c56b2e/Screenshot%20from%202021-09-28%2012-22-47.png "Logo Title Text 1")

Also ssh to the server and check for the jenkins server to be deployed over docker.

```
ubuntu@ip-172-31-84-130:~$ sudo docker ps
CONTAINER ID   IMAGE         COMMAND                  CREATED          STATUS          PORTS                                                                                                                               NAMES
c0d1ae80c36f   opt_jenkins   "/sbin/tini -- /usr/…"   40 minutes ago   Up 40 minutes   0.0.0.0:8443->8443/tcp, :::8443->8443/tcp, 0.0.0.0:9586->8080/tcp, :::9586->8080/tcp, 0.0.0.0:8082->50000/tcp, :::8082->50000/tcp   opt_jenkins_1
```
Also to access the jenkins dashboard 
IP:9586

![output2](https://github.com/AyushGupta88/Ansible-jenkins/blob/35824ad12d9f4095f527635e4508fb653f31bf70/image_2021_09_28T07_04_18_832Z.png)
  
  
