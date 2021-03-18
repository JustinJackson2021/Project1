## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.


(https://user-images.githubusercontent.com/80436108/111563317-5e602680-875d-11eb-9586-27d48e1394d7.jpg)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YMAL file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/JustinJackson2021/Project1/tree/main/Ansible

1. Ansible Configuration
2. Ansible ELK Installation and VM Configuration
3. Ansible Filebeat Playbook
4. Ansible Filebeat Config file
5. Ansible Metricbeat Playbook
6. Ansible Metricbeat Config file

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly protected, in addition to restricting traffic to the network.
What aspect of security do load balancers protect? 

Azure Load Balancer operates at layer four of the Open Systems Interconnection (OSI) model and protects servers from getting overloaded and possibly breaking down. If a single server goes down, the load balancer redirects traffic to the remaining online servers. When a new server is added to the server group, the load balancer automatically starts to send requests to it. In other words, load balancing improves service availability and helps prevent downtimes.

What is the advantage of a jump box?_

Jump box prevents Azure VMs from being exposed to the public. This means that this will be the entry point connecting via Remote Desktop Protocol (RDP) from the on-premise network. It also helps to open only one port instead of several ports to connect different virtual machines present in the Azure cloud.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to thelogs and system traffic.

What does Filebeat watch for?

Filebeat watches and monitors the log files or locations that users specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing. Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on the server.

What does Metricbeat record?

Metricbeat is a lightweight shipper that records and periodically collects metrics from the operating system and from services running on the server and takes the metrics and statistics that it collects and ships them to the output that users specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
(http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| web-1    | Server   | 10.0.0.8   | Linux            |
| web-2    | Server   | 10.0.0.9   | Linux  
| web-3    | Server   | 10.0.0.10  | Linux   
| Elk-Host | Monitoring | 10.1.0.4 | Linux      |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 

Machines within the network can only be accessed by Jump-Box-provisioner.
- Which machine did you allow to access your ELK VM? What was its IP address?
10.0.0.4(Jump box private IP)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |                      |
| Web-1    | No                  |   10.0.0.4           |
| Web-2    | No                  |   10.0.0.4           |
| Web-3    | No                  |   10.0.0.4           |
| Elk-Host | No                  |   10.0.0.4           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?

1.Free: Ansiable is an open source tool

2.Very simple to set up an use: dont really need any speical coding skills to use the playbook

3.Powerful: allows users to model highly complex IT work

4.Flexible: User can customize it to their needs and and can access it no matter where it is deployed.

5.Agentless: Don't need to install software or firewall ports. Also don't need to set up seperarte manegment structure.

6.Efficent: Don't need to install any extra software.

The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
1. Install docker.io
2. Install pip3
3. Install Docker python module
4. Increase virtual memory
5. Download and launch a docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/80436108/111563537-beef6380-875d-11eb-832f-18676ce3c5c2.png)



### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name       | IP Adrress  |       
| Web-1      | 10.0.0.8    |
| Web-2      | 10.0.0.9    |
| Web-3      | 10.0.0.10   |


We have installed the following Beats on these machines:
1. filebeat
2. metricbeat

These Beats allow us to collect the following information from each machine:

Filebeat - collects data about a system like log events, and will send them to a monitoring system.

Metricbeat - collects metrics and statistics data and sends them to a specified output, like Elasticsearch and Logstash.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to Ansible.
- Update the host file to include webservers and ELK.
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

nano ansible.cfg
add the machine, its IP, and ansible_python_interpreter=/usr/bin/python3 to the hosts
Ctrl + x to exit file
in the folder that install-elk.yml is in, run: cp install-elk.yml /etc/ansible
nano install-elk.yml /etc/ansible
name: installing elk hosts: [your_machine]
Ctrl + x to exit file
ansible-playbook install-elk.yml
