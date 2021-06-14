## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![RedTeam-Cloud-Network](https://github.com/Enrique1003/CyberSecurity/blob/main/Diagrams/RedTeam-Cloud-Network.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

[ELK.yml](https://github.com/Enrique1003/CyberSecurity/blob/main/Ansible/ELK.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available in addition to restricting in-bound access to the network.

- Load balancers can use the off- loading function distribute malicious traffic caused by DDoS attacks by shiftiing the traffic from the main client server to a public cloud provider.  

- An advantage of using a jump box is that it is a secure node that all admins first connect to before executing any task thats secured and monintored.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the jumpbox and system network.
- Filebeat watches changes to files on the machine.
- Metricbeat records metrics from the operating system and from services running on the server. 

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
|Jump Box  |Gateway   |10.0.0.7    | Linux            |
|Web-1     |Webserver |10.0.0.8    | Linux            |
|Web-2     |Webserver |10.0.0.9    | Linux            |
|ELK       |Monitoring|10.1.0.4    | Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box proviner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 5061 port, Kibana, 20.81.160.43

Machines within the network can only be accessed by jump box provisioner.
- My host machine was allowed access to the ELK VM. (host public ip:184.103.201.201)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
|Jump Box  |Yes                  |184.103.201.201       |
|Web-1     |No                   |10.1.0.4              |
|Web-2     |No                   |10.1.0.4              |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

- Efficient in terms of not needing to install any extra software which will allow more space for resources on a server.
- Free open-source tool.
- Flexibility allows you to structure and setup the application environment anywhere it is deployed.

The playbook implements the following tasks:
- Install docker.io
- Install pip3
- Install Docker python module
- Increase virtual memory
- Download/launch a docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK-docker-ps.PNG](https://github.com/Enrique1003/CyberSecurity/blob/main/Diagrams/ELK-docker-ps.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.8
- Web-2 10.0.0.9

We have installed the following Beats on these machines:
- Microbeats

These Beats allow us to collect the following information from each machine:
- Filebeats which collects data about the file system, and Metricbeat. Metricbeatvcollects metrics from a system or services running on the server such as uptime or Apache.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to Ansible control node.
- Update the hosts file to include webserver and elk.
- Run the playbook, and navigate to Kibana http://[Host IP]/app/kibana#/home to check that the installation worked as expected.

###############################
- The files for the playbook are the filebeat and metricbeat .yml file. you obtain these by using these 2 commands:
1. 'curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/filebeat-config.yml)'
2. 'curl https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat > /etc/ansible/metricbeat-config.yml'

- You will need to cd into the filebeat and metric beat files in [/etc] folder to edit thier respective.config files. then add the private ip's of the web servers under [webservers] and add [elk] to establish the elk network followed by the elk private ip directly under it that.
- To check that the ELK server is running, enter http://[Host IP]/app/kibana#/home in your address bar.
