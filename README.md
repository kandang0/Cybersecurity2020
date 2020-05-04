# Cybersecurity2020
# Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.
 Virtual Network Diagram
![alt text](https://github.com/kandang0/Cybersecurity2020/blob/master/Diagrams/Diagram1.jpg "Virtual Network Diagram")
 
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the Playbook file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
•	Description of the Topology
•	Access Policies
•	ELK Configuration 
o	Beats in Use
o	Machines Being Monitored
•	How to Use the Ansible Build
## I.	Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA Vulnerable Web Application.
Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
Security advantage of load balancers 
Load balancers protect the availability aspect of security. They provide the features needed to counter security threats like high-volume DDoS attacks. Load balancers also have features and policy controls to stop bad traffic from ever reaching the application, including rate limiting and URL filtering.
Security advantage of a jump box
A jump boxes both is a highly secure computer used for completing admin tasks or used as jumping off points to other computers and networks. It has strong computer security controls applied, far stricter than would normally be applied in the regular environment. It is not connected to unsecure computers and is less likely to pick up exploits. It is used to perform administrative tasks on mission-critical resources.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system logs.
What does Filebeat watch for?
Filebeat log information about the file system, including which files have changed and when.
What does Metricbeat record?
Metricbeat record system performance metric such as CPU usage, memory, and load. In dockerized environments, Metricbeat can be installed on a host for monitoring container performance metrics.
The configuration details of each machine may be found below:
| Name                      | Function                    | IP Address                 |   Operating System
| --------------------------|:---------------------------:|:--------------------------:|:------------------- |
| Jump-Box-Provisioner      | Gateway                     | 10.0.0.4/Dynamic Public IP |   Linux
| DVWA-VM1                  | Web Server                  | 10.0.0.5/13.77.173.56      |   Linux
| DVWA-VM2                  | Backup Web Server  	  | 10.0.0.7/13.77.173.56      |   Linux
| Elk-Server                | Network Security Monitoring | 13.77.139.204              |   Linux
 
## II.	Access Policies
The machines on the internal network are not exposed to the public Internet.
All the machines in the virtual network can be accessed from a container inside the Jump-Box-Provisioner.
The jump-Box-Provisioner can be accessed from a single public IP address trough ssh connection on port 22.
This single public IP is also used to access Kibana on the ELK server to visualize Elasticsearch data and navigate the Elastic Stack so you can do anything from tracking query load to understanding the way requests flow through the DVWA web apps.
HTTP traffic towards the web servers is filtered through the load balancer before accessing the web application hosted inside DVWA-VM1 and DVWA-VM2.
DVWA-VM1 and DVWA-VM2 do not have a built-in public IP. They can be reached through the public IP of the load balancer, 13.77.173.56.

A summary of the access policies in place can be found in the table below.
| Name                      | Publicly Accessible  | Allowed IP Addresses       |   
| --------------------------|:---------------------:|:--------------------------:|
| Jump-Box-Provisioner      | No                    | Home Public Ip             |  
| DVWA-VM1                  | Yes                   | Any                        |  
| DVWA-VM2                  | Yes  	            | Any                        |  
| Elk-Server                | No                    | Home Public IP             |   



		
		
## III.	Elk Configuration
A free open-source tool, amazingly simple to set up and use, yet powerful, Ansible, was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it is efficient and increases productivity and reliability.
Ansible is agentless and does not require any other software or firewall ports on the ELK server or the DVWA machines.
Automating configuration with Ansible frees IT administrators to focus on efforts that help deliver more value to the business by spending time on more important tasks.
The playbook implements the following tasks:
1.	Download the .deb file from artifacts.elastic.co.
2.	Install the .deb file using the dpkg command shown below:
dpkg -i filebeat-7.4.0-amd64.deb
3.	Copy the Filebeat configuration file from your Ansible container to your ELK VM.

4.	Run the following commands:
•	./filebeat modules enable system
•	./filebeat setup
•	./filebeat -e

The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.
 Docker ps: 
![alt text](https://github.com/kandang0/Cybersecurity2020/blob/master/Diagrams/Picture1.JPG "Docker ps")
###Target Machines & Beats
This ELK server is configured to monitor the following machines:
1.	DVWA-VM1		IP Address: 10.0.0.5
2.	DVWA-VM2		IP Address: 10.0.0.7
We have installed the following Beats on these machines:
Filebeat and metricbeat were successfully installed on DVWA-VM1 and DVWA-VM2.
These Beats allow us to collect the following information from each machine:
Filebeat as "A lightweight shipper for forwarding and centralizing log data. It helps you keep the simple things simple by offering a lightweight way to forward and centralize logs and files. On the other hand, Metricbeat is detailed as "A Lightweight Shipper for Metrics".
## IV.	Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
SSH into the control node and follow the steps below:
•	Copy the playbook file filebeat-playbook.yml to the ansible container.
•	Update the filebeat configuration file /etc/ansible/files/filebeat-configuration.yml  file to include your ELK server's IP address: 13.77.139.204
•	Run the playbook, and navigate to http:// http://13.77.139.204:5601:5601 to check that the installation worked as expected.
To run the playbook, from the Ansible directory, enter the command: 
ansible-playbook filebeat-playbook.yml
Click on the link below to access the configuration files used to deploy the virtual network.
filebeat-laybook.yml
filebeat-configuration.yml
metricbeat-playbook.yml
metricbeat-configuration.yml
