### Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://github.com/Charles12jr/Project-1/blob/main/Diagrams/Complete_Network_Diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML  file may be used to install only certain pieces of it, such as Filebeat.

- [filebeat-config.yml](https://github.com/Charles12jr/Project-1/blob/main/Ansible/filebeat-config.yml)
- [filebeat-playbook.yml](https://github.com/Charles12jr/Project-1/blob/main/Ansible/filebeat-playbook.yml)
- [metricbeat-config.yml](https://github.com/Charles12jr/Project-1/blob/main/Ansible/metricbeat-config.yml)
- [Metricbeat-playbook.yml](https://github.com/Charles12jr/Project-1/blob/main/Ansible/Metricbeat-playbook.yml)
- [Install-Elk.yml](https://github.com/Charles12jr/Project-1/blob/main/Ansible/Install-Elk.yml)
- [Ansible-config.yml](https://github.com/Charles12jr/Project-1/blob/main/Ansible/Ansible-cfg.yml)
- [Install-docker.yml](https://github.com/Charles12jr/Project-1/blob/main/Ansible/Install-docker.yml)


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure in addition to restricting access to the network.

- Load balancers establish redundancy to enhance availability for the Network
- The Advantage of a jump box is that it creates one secure entry point into the Network in which all admins connect to initially before launching any administrative task.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.

- Filebeat monitors for changes in system files, allowing real-time detection of important changes
- collects metrics from the operating system and from services running on the server

The configuration details of each machine may be found below.

| Name       	| Function   	| IP Address 	| Operating System 	|
|------------	|------------	|------------	|------------------		|
| Jumpbox    	| Gateway    	| 10.0.0.9   	| Linux ubuntu 18.04 	|
| Web-1      	| Web Server  	| 10.0.0.6   	| Linux ubuntu 18.04 	|
| Web-2      	| Web Server  	| 10.0.0.8   	| Linux ubuntu 18.04 	|
| Elk-Server 	| Monitoring 	| 10.1.0.4   	| Linux ubuntu 18.04 	|




### Access Policies

The machines on the internal network are not exposed to the public Internet. 

* Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
99.156.170.50 (Work Station) 

Machines within the network can only be accessed by ssh from jumpbox.

The machine allowed access to the ELK VM is work station and Jump Box
* The IP Address is 99.156.170.50 (Work Station)
* The IP Address is 10.0.0.9 (Jump box)

A summary of the access policies in place can be found in the table below.

| Name       	| Public Accessible 	| Allowed IP Address 	|
|------------	|--------------------	|--------------------	|
| Jumpbox    	| Yes                	| 99.156.170.50      	|
| Web-1      	| No                	 	| 10.0.0.9    		|
| Web-2      	| No               	  	| 10.0.0.9   	 	|
| Elk-Server 	| No		         	| 10.0.0.9	     	|


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because allows us to quickly and repeatedly deploy our container, ensuring we have a consistent deployment that eliminates most human error


The playbook implements the following tasks:

* Install docker.io
* Install python-pip
* Install the docker module using pip
* Increases the virtual memory of our ELK VM
* Downloads and launches the sebp/elk container over ports 5601, 9200, and 5044.


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![alt text](https://github.com/Charles12jr/Project-1/blob/main/Images/docker_ps_output.PNG)

Target Machines & Beats

This ELK server is configured to monitor the following machines:
* Web-1 10.0.0.6
* Web-2 10.0.0.8

We have installed the following Beats on these machines:
* Filebeat and Metricbeat have been installed.

These Beats allow us to collect the following information from each machine:


- Filebeat collects log data and shows them in the monitoring clusters. An example of such are the logs produced from the MySQL database
Metricbeat collects metrics and statistics and shows them in the output specified, for example Elasticsearch or Logstash. An example of such is cpu usage, which can be used to monitor the system health.

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

1.SSH into the control node and follow the steps below:

2.Copy the Install-Elk.yml file to your /etc/ansible directory.

3.Update the host file to include the IP Addresses of your Web-1, Web-2, and ELK server as well as assign python3 as the interpreter.

4.Run the playbook, and navigate to your ELK server to check that the installation worked as expected.

Which file is the playbook? The playbook files are:

* Install-Elk.yml - used to install ELK Server

* filebeat-playbook.yml - Used to install and configure Filebeat on Elk Server and DVWA servers

* metricbeat-playbook.yml - Used to install and configure Metricbeat on Elk Server and DVWA servers

Where do you copy it?

* /etc/ansible/

Which file do you update to make Ansible run the playbook on a specific machine?

* /etc/ansible/hosts.cfg

How do I specify which machine to install the ELK server on versus which to install Filebeat on?

* In /etc/ansible/hosts you tell it where you want each to be installed on either the ElkServers or webservers (FileBeat)

Which URL do you navigate to in order to check that the ELK server is running?

- http://[your.ELK-VM.External.IP]:5601/app/kibana

