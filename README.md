# gt-project1
Repository featuring core cybersecurity milestones in Linux, network diagrams and cloud security
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
 ~/testproject/gt-project1/Diagrams/Network Diagram
 ![Network Diagram](https://user-images.githubusercontent.com/89884747/134429253-b017b4b9-9e6e-4bdf-bd9d-061c8bd2ac2b.PNG)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

 ~/testproject/gt-project1/Ansible/ansible.config

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- Restricting access to network and permitting server availability via directing network traffic evenly to different servers to allow balanced performance.
- What is the advantage of a jump box? Provides secure access to the back end of servers

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system Files.
- What does Filebeat watch for? Collects log events and forwards them either to Elasticsearch or Logstash
- What does Metricbeat record? Collects metrics from the OS and running services on the server and forwards them to Elasticsearch or Logstash

The configuration details of each machine may be found below.

| Name         | Function                        | IP Address | Operating System |
|--------------|---------------------------------|------------|------------------|
| Jump Box     | SSH Backend                     | 10.0.0.4   | Linux            |
| ELK Server   | Collect/Analyze Security Events | 10.1.0.4   | Linux            |
| Web Server 1 | Web Host                        | 10.0.0.7   | Linux            |
| Web Server 2 | Web Host                        | 10.0.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
NA (IP Address private for security reasons)

Machines within the network can only be accessed by the jumpbox.
Jumpbox
Public IP: 13.66.130.8
Private IP: 10.0.0.4

A summary of the access policies in place can be found in the table below.
| Name     | Public Accessible           | Allowed IP Address(s) |
|----------|-----------------------------|-----------------------|
| Jump Box | SSH Backend (22) YES        | NA (PRIVATE)          |
| WEB 1,2  | NO                          | 52.156.118.133 WEB LB |
| WEB LB   | HTTP PORT 80 YES (RED TEAM) | NA                    |
| ELK      | Access-Kibana-port 5601 YES | NA                    |
| ELK      | HTTP  YES Port 9200         | 10.0.0.0/16           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because this may help IT professionals program services automatically without the need for constant manual script writing
What is the main advantage of automating configuration with Ansible? Ansible automation reduces time to get new servers and services up and running, especially in environments where servers require regular removal and setup.

The playbook implements the following tasks:
-Installs Docker to the indicated web server
-Installs and builds a docker image on the webserver
-Installs Python3_pip to server
-Installs more memory to run ELK memory intensive services
-Installs docker python module
-Downloads and launches an ELK container and indicates specific ports to operate on
-Enable Docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
~/testproject/gt-project1/Diagrams/elk_image.png
![elk_image](https://user-images.githubusercontent.com/89884747/134429421-e7462f1d-84f4-4f1d-8ccb-4512f6de9e0f.PNG)



### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-10.0.0.7
-10.0.0.6

We have installed the following Beats on these machines:
-installation of Filebeat and Metricbeat is on the following systems: Web 1, Web 2



These Beats allow us to collect the following information from each machine:
-Filebeat monitors data, including log files and collets these log events and forwards them to Elasticsearch and or logstash
-Metricbeat periodically collects data from servers--this data includes metrics on CPU, memory and other information related to services that may run on a server


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible.
- Update the host file to include the IPO's of the current servers you are configuring
- Run the playbook, and navigate to http://{ELK VM IP}.5601 to check that the installation worked as expected.
- Playbooks are usually located in .yml format i.e. filebeat.yml and metricbeat.yal

- _Which file is the playbook? Where do you copy it?
- Both the filebeat and metricbeat play books are copied to the /ect/ansible directoies on the server machines
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- Update the hosts.txt, filebeat-config.yml and metricbeat-config.yml files to reflect the ports ( 5601,9200 ) and server IP address for the web servers 10.0.0.6, 10.0.0.7, 10.1.0.4
- _Which URL do you navigate to in order to check that the ELK server is running?
- http://[ELK-VM up]:5601
