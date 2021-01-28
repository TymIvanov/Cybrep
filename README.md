# Cybrep
UCB

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Arrakis Diagram](https://drive.google.com/file/d/1G23dahiCKDiUFJQ3u8Cq67qfFTlxXAOE/view?usp=sharing)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - -- install-elk.yml
 
       filebeat-config.yml
       metricbeat-config.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly avalible, in addition to restricting access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

A load balancer defends an organization against distributed denial-of-service (DDoS) attacks.
SSH from a JumpBox to the target host allows the use of insecure protocols to manage servers without creating special firewall rules or exposing the traffic on the inside network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- _TODO: What does Filebeat watch for? It monitors the log files or locations, collects log events, and forwards them either to Elasticsearch or Logstash.
- _TODO: What does Metricbeat record? Metricbeat takes the metrics and statistics that it collects and sends them to the output that you specify, such as Elasticsearch or Logstash.
The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| name      | function      | IP address             | operating system |
|-----------|---------------|------------------------|------------------|
| PAJumpbox | gatewas       | 13.87.128.102/10.0.0.7 | Linux/Ansible    |
| Web-1     | webserver     | 10.0.0.5               | Linux/DVWA       |
| Web-2     | webserver     | 10.0.0.6               | Linux/DVWA       |
| Web-3     | webserver     | 10.0.0.8               | Linux/DVWA       |
| ELK       | ELK-server    | 10.1.0.4               | Linux            |
| LOAD BL   | Load balancer | 40.78.100.244          | Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses is IP of Tym's personal machine

Machines within the network can only be accessed by JumpBox and Tym's personal machine.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address? 
JumpBox 10.0.07

A summary of the access policies in place can be found in the table below.

| name          | Publicity Accessible | Allowed IP address       |
|---------------|----------------------|--------------------------|
| PAJumpbox     | no                   | Tym's public IP          |
| Web-1         | no                   | 10.0.0.7                 |
| Web-2         | no                   | 10.0.0.7                 |
| Web-3         | no                   | 10.0.0.7                 |
| ELK           | no                   | 10.0.0.7/Tym's public IP |
| Load Balancer | no                   | Tym's public IP          |      |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible? It allows deploy multiple containers at once.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Specify a different group of machines as well as a different remote user
 - name: Config elk VM with Docker
    hosts: elk
    remote_user: sysadmin
    become: true
    tasks:

-  install the following services:
   `docker.io`
   `python3-pip`
   `docker`, which is the Docker Python pip module.

  - Launching and Exposing the container with these published ports:
     `5601:5601` 
     `9200:9200`
     `5044:5044`
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![alt image] (https://ibb.co/jDLNMcC)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
  10.0.0.5
  10.0.0.6
  10.0.0.8

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
Web-1
Web-2
Web-3
Elk

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat collects logs of events and Metricbeat coleccts metrics and system statistics 
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-yelk.yml file to /etc/ansible
- Update the hosts file to include ELK Vm
- Run the playbook, and navigate to web browser/kibana website to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it? YAML script could ne written for specifific machine. etc/ansible
- _Which file do you update to make Ansible run the playbook on a specific machine?
 /etc/ansible# curl -L -O https://ansible.com/  > ansible.cfg
 /etc/ansible# nano ansible.cfg
Which URL do you navigate to in order to check that the ELK server is running?
172.17.0.1:5601/app/kibana#/home?_g(}_As a 
**Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

Download Filebeat playbook usng this command:
curl -L -O https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml

Update the filebeat-playbook.yml file to include installer
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb

Download Metricbeat playbook using this command:
curl -L -O https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat > /etc/ansible/files/metricbeat-config.yml

curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.6.1-amd64.deb

use nano to updaye config files and ansible-playbook to play particular playbook.
