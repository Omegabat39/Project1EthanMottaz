# Project1EthanMottaz
Unit 13-Project1
![Vnet(Final)EthanMottaz drawio](https://user-images.githubusercontent.com/97130195/167510489-3a29de4d-aac6-427f-9150-32b1aa0e5b40.png)


## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.



These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _yml and config_ file may be used to install only certain pieces of it, such as Filebeat.

  - Omegabat39/Project1EthanMottaz/Ansible

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _Availble_, in addition to restricting _Traffic_ to the network.
- What aspect of security do load balancers protect? What is the advantage of a jump box?
- _Availability, Web Traffic and Web Security

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _Data____ and system _Logs_.
- What does Filebeat watch for?
  _data about file systems_
- What does Metricbeat record?
  _machine metric data_

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                   | Function     | IP Address            | Operating System |
|------------------------|--------------|-----------------------|------------------|
| Jump-Box-  Provisioner | Gateway      | 10.0.0.4/40.69.136.125| Linux            |
| Web-1                  |Web Server    | 10.0.0.5              | Linux            |
| Web-2                  |Web Server    | 10.0.0.6              | Linux            |
| Web-3Elk               |   ELK        | 10.1.0.4/40.87.111.127| Linux            |
| ClassLB                |Load Balancer |40.77.69.8             | Linux            |
| Workstation            |Access Control|173.28.119.51          | Mac              |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _Host_machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Add whitelisted IP addresses_
 173.28.119.51 through TCP 5601

Machines within the network can only be accessed by _ Workstation and Jump-Box-Provisioner_.
- Which machine did you allow to access your ELK VM? What was its IP address?_
 -Jump-Box-Provisioner IP : 10.0.0.4 via SSH port 22
 -Workstation        :173.28.119.51 via port TCP 5601
      
A summary of the access policies in place can be found in the table below.

| Name                | Publicly Accessible |        Allowed IP Addresses        |
|---------------------|---------------------|------------------------------------|
|Jump-Box-Provisioner |No                   | 173.28.119.51 on SSH 22            |                |Web-1                |No                   | 10.0.0.4 on SSH 22                 |
| Web-2               |No                   | 10.0.0.4 on SSH 22                 |
| Web-3Elk            |No                   | 173.28.119.51 on SSH 22            |
| ClassLB             |No                   | 173.28.119.51 on SSH 22            |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?_
-Ansible lets you quickly and easily deploy multitier apps. It is all automated.You list the   tasks and can write a playboo. Ansible will do the rest to make sure the systems are how yo      want.

The playbook implements the following tasks:
-In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Specify group of machines and user
- Increase system memory
- Installs services
- launchs ports and exposes the ports
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img width="1440" alt="Docker-PS-EM" src="https://user-images.githubusercontent.com/97130195/148587400-306be96a-b1b0-4a54-a64d-998680b2d7ae.png">


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-List the IP addresses of the machines you are monitoring_

-Web-1 IP: 10.0.0.5
-Web-2 IP: 10.0.0.6

We have installed the following Beats on these machines:
- Specify which Beats you successfully installed_
- Filebeat: log events
  Metricbeat: metric stats and system stats

These Beats allow us to collect the following information from each machine:
-In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat montiors for log events such as server logs; Metricbeat collects metric data such as MySQL and records it on elastic search. These finding may show up on kibana.
(other requested screenshots)
<img width="1440" alt="Metricbeat-scree shot-EM" src="https://user-images.githubusercontent.com/97130195/148586569-1b9dd71d-f77d-4ea3-9bfa-802208ccb418.png">
<img width="1440" alt="Filebeat_screenshotEM" src="https://user-images.githubusercontent.com/97130195/148586849-261167ef-57f9-4c82-8eef-d09ac2c17836.png">
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _/etc/ansible/files/filebeat-config.yml_ file to _/etc/filebeat/filebeat-playbook.yml_.
- Update the _filebeat-playbook.yml_ file to include... curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb
- Run the playbook, and navigate to __Kibana > Logs : Add log data > System logs > 5:Module Status > Check__ to check that the installation worked as expected.

_  Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?
-  playbook is in root@bb16ebc0f579:/etc/ansible/files/filebeat-config.yml and nano /etc/ansible/roles/filebeat-playbook.yml

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?
root@bb16ebc0f579:/etc/ansible# curl -L -O https://ansible.com/  > ansible.cfg
root@bb16ebc0f579:/etc/ansible# nano ansible.cfg

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

Work cited for additional information:

Collecting Elasticsearch log data with Filebeat: Elasticsearch guide [7.16]. Elastic. (n.d.). Retrieved January 7, 2022, from https://www.elastic.co/guide/en/elasticsearch/reference/current/configuring-filebeat.html 

How metricbeat worksedit. Elastic. (n.d.). Retrieved January 7, 2022, from https://www.elastic.co/guide/en/beats/metricbeat/current/how-metricbeat-works.html 
