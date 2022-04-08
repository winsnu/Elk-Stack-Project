## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram](Diagrams/Cloud%20Security.drawio-2.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible-playbook file may be used to install only certain pieces of it, such as Filebeat.

  - [install-elk.yml](Ansible/Install-elk.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- What aspect of security do load balancers protect? 
    The load balancer protects from DDos attacks, SSL offload, authenticate using ID, protects applications from threats, traffic compression and traffic caching.
- What is the advantage of a jump box?
    The jump box acts as an audit for traffic and a point where user accoutns can be managed.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- What does Filebeat watch for?
    Filebeat monitors and collects logs and forwards that info to Elasticsearch or Longstash.
- What does Metricbeat record?
    Metricbeat records metrics and statistics and forwards that info to Elasticsearch or Longstash.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump-Box | Gateway  | 10.1.0.4   | Linux            |
| Web-1    | Server   | 10.1.0.5   | Linux            |
| Web-2    | Server   | 10.1.0.6   | Linux            |
| Elk-VM   | Server   | 10.0.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- Personal IP Address

Machines within the network can only be accessed by Jump-Box.
- Which machine did you allow to access your ELK VM? 
    Jump-Box
- What was its IP address?
    10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses |
|---------------|---------------------|----------------------|
| Jump-Box      | Yes                 | 10.1.0.4, Public IP  |
| Web-1         | No                  | 10.1.0.5             |
| Web-2         | No                  | 10.1.0.6             |
| Elk-VM        | Yes/No              | 10.0.0.4, Public IP  |
| Load-Balancer | Yes                 | 20.213.37.53         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?
    Ansible is easy to set up, use, read, and no coding skills required.

The playbook implements the following tasks:
- name: set maximum map count in sysctl/systemd
- name: docker.io
- name: install pip3
- name: install Docker module
- name: download and launch Elk

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[docker ps](Linux/docker%20ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.1.0.5 (Web-1)
- 10.1.0.6 (Web-2)

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat: Monitors and collects log files and events and forwards them to Elasticsearch or Logstash.
- Metricbeat: Takes the metrics and statistics collected and sends them to Elasticsearch or Logstash.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
[filebeat-playbook.yml](Ansible/filebeat-playbook.yml)
[metricbeat-playbook.yml](Ansible/metricbeat-playbook.yml)

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files
- Update the /etc/ansible/hosts file to include the IP address of webservers and the Elk-Stack
- Run the playbook, and navigate to http://personalIP:5601/ to check that the installation worked as expected.

- Which file is the playbook? 
    [filebeat-playbook.yml](Ansible/filebeat-playbook.yml)
- Where do you copy it?
    Into the etc/ansible/files folder
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
    You update the [hosts](Ansible/hosts) file by adding the private IP of the specific machine
- Which URL do you navigate to in order to check that the ELK server is running?
    http://VM-IP:5601/app/kibana

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.

Open terminal, SSH azadmin@JumpBox-IP - (SSH into your JumpBox VM)

sudo docker container list -a - (list containers on your VM)

sudo docker start "container-name" - (start your specified container)

docker attach "container-name" - (attach your container)

cd /etc/ansible/ - (navigate to the ansible directory)

curl https://github.com/winsnu/Elk-Stack-Project/blob/main/Ansible/Install-elk.yml - (to download playbook file)

nano hosts - (update IP on [webservers][elk][elkservers] Example: 10.0.0.4 ansible_python_interpeter=/usr/bin/python3

nano ansible.cfg - (add remote_user=azadmin to which server you want to use)

ansible-playbook my-playbook.yml - (ansible-playbook is the command to run the file)
