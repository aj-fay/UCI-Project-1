## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![AWSCloudELK](https://github.com/aj-fay/UCI-Project-1/blob/master/UCI-Project-1/Images/Elk-Diagram.drawio.png)

These files have been tested and used to generate a live ELK deployment on AWS. They can be used to either recreate the entire deployment 
pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - [Filebeat Playbook](https://github.com/aj-fay/UCI-Project-1/blob/master/UCI-Project-1/Repository/filebeat-playbook.yaml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient and responsive, in addition to restricting unwanted traffic to 
the network.
- Load balancers create greater availability to the servers. They allow web traffic, memory capacity, and CPU load to be
  distributed accross multiple servers in order to keep up performance and efficiency.
- The advantages of having a JumpBox include:
  - Improved security by only allowing SSH from a host computer that contains the proper key
  - Ability to run playbooks across multiple machines as a host
  - Giving the ability of customization in order to enhance network security
  - Centralizaed administration management

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems and system metrics.
- Filebeat watches any log files or specified locations and sends them to Elasticsearch or Logstash.
- Metricbeat records metrics from the OS and other services running on the server.


| Name       | Function        | IP Address   | Operating System    |
|------------|-----------------|--------------|---------------------|
| Jump Box   | Gateway         | 172.--.-.76  | Amazon Linux 2      |
| WebServer1 | Application     | 172.--.--.23 | Amazon Linux 2      |
| WebServer2 | Application     | 172.--.--.50 | Amazon Linux 2      |
| ELK Server | Database Logger | 172.--.--.66 | Ubuntu Server 20.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:
- My personal IP 47.---.-.---

Machines within the network can only be accessed by SSH on port 22 with the JumpBox.
- The JumpBox is the only machine that is allowed to access the ELK VM with the IP of 172.--.-.76

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| JumpBox    |          No         |      42.---.-.---    |
| WebServer1 |         Yes         |       0.0.0.0/0      |
| WebServer2 |         Yes         |       0.0.0.0/0      |
| ELK        |          No         |      172.--.-.76     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- There would be less human error and time involved in order to configure the ELK machine.

The playbook implements the following tasks:
- Download docker.io
- Increase virtual memory
- Install python3-pip
- Install docker python module
- Download and launch ELK web container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK-dockerps](https://github.com/aj-fay/UCI-Project-1/blob/master/UCI-Project-1/Images/ELK-dockerps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- WebServer1: 172.--.--.23
- Webserver2: 172.--.--.50

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects log messages and other specified log events and sends them to a designated output. You would be able to see audit
  logs, gc logs, deprecation logs, slow logs, and server logs.
- Metricbeat collects metrics and statistics of memory, CPU, or any data related to the specified target.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node
provisioned: 

SSH into the control node and follow the steps below:
- Copy the "filebeat-config.yml" file to "ELK VM."
- Update the "hosts" file to include web server private IP addresses and ELK server private IP address. You can specify the machines by
  creating two different host groups; one for web servers and another for elk.
- Run the playbook, and navigate to Kibana via <ELK public IP:5601> to check that the installation worked as expected.


