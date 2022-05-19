## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

  - Images/Network Diagram

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - pentest-playbook.yml
  - elk-playbook.yml
  - filebeat-playbook.yml
  - metricbeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration                                         20.92.215.38
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
  -Having a load balancer in place ensures the website availability even if 1 web server goes down.
  -Having a jump box limits access to more vulnerable systems. It is limited by IP address accessing it and ssh key to prevent
   brute force password cracking attempts.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system metrics.
  - Filebeat monitors files on the Elk Server and reports any changes.
  - Metricbeat monitors certain metrics of the system itself (cpu, ram, disk space, etc) and reports changes.

The configuration details of each machine may be found below.


| Name    | Function       | IP Address | Operating System |
|---------|----------------|------------|------------------|
| Jumpbox | Gateway        | 10.0.0.4   | Linux            |
| Web-1   | DVWA Container | 10.0.0.5   | Linux            |
| Web-2   | DVWA Container | 10.0.0.6   | Linux            |
| Elk     | Elk Server     | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
  - 24.42.190.30

Machines within the network can only be accessed by SSH.
- The jumpbox can access the Elk server but only through SSH. The IP Address for the jumpbox is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name    | Publicly Accessible | Allowed IP Address |
|---------|---------------------|--------------------|
| Jumpbox | YES                 | 24.42.190.30       |
| Web-1   | NO                  |                    |
| Web-2   | NO                  |                    |
| Elk     | NO                  |                    |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
  - Configuring with Ansible is repeatable no matter how much you grow.

The playbook implements the following tasks:
  - uses apt to install Docker.io
  - uses apt to install python3-pip
  - uses pip to install docker module
  - increases memory to run Elk
  - downloads and launches Elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

  - Images/Elk Docker

### Target Machines & Beats

This ELK server is configured to monitor the following machines:
  - Web-1 10.0.0.5
  - Web-2 10.0.0.6

We have installed the following Beats on these machines:
  - Filebeats
  - Metricbeats

These Beats allow us to collect the following information from each machine:

  - These beats collect data from files that may be accessed or changed on the system as well as metrics of the system (ex cpu usage, mem usage, storage capacity). We would expect to see
    a log created for example if the cpu usage spiked because of a large file being downloaded.

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files
- Update the filebeat-config.yml file to include IP Address of Elk server
- Run the playbook, and navigate to the public IP address of the Elk server (use port 5601) to check that the installation worked as expected.


  -Which file is the playbook? Where do you copy it?  https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb
  -Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
   You modify the /etc/ansible/hosts file and edit the ip addresses. There is a group for webservers and there is one for Elk. Placing the correct ip address in the correct group will
   ensure that filebeat gets installed on the correct device.
  -Which URL do you navigate to in order to check that the ELK server is running? Navigate to the public IP address of the ELK Server using the port 5601 to determine if ELK is running.

  - In order to run the playbook you will need to run this command # ansible-playbook /etc/ansible/filebeat-config.yml  and   # ansible-playbook /etc/ansible/metricbeat-config.yml # cyberresource