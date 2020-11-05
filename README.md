# README file for ncd-ansible-2 repository
---
## Use Cases 

### UseCase1:
Your Manager asks you to write a playbook which can setup the Lampstack environment,same playbook will be used
in different environments.

Your playbook should create the below services:
1) Install Apache.
2) Install Php module.
3) Start the apache service.
4) Copy index.php file into apache root directory.
5) Install Mariadb server package.
6) Start mysql server.
7) Install python mysql package.
8) Create a Database.
9) Create a Database user.
10) Copy dumb data.
11) Insert sample data in database.
12) Install mysql extention for php.
13) Restart Apache service.
14) Deploy sample php file in apache root directory.
#### Description
Many of the developers work on temporary Lampstack environments
to deploy there php code and test on servers.
We get multiple requests per day to create such environments with minor customizations.
We have designed playbooks to create the environment as per the requirements.
Before running the playbook, we adjust the variables file with required parameters and run it to create the environment.
This playbook creates the environment with PHP,Apache and Mariadb, and also this palybook will create a dummy user and 
database to test and Samaple Data is dumped in apache root directory.
### Prerequisites:
1) Ansible server.
2) ubuntu slave servers.
### How to run the Ansible-playbook:
--> ansible-playbook playbook.yml
### How to access application on browser:
--> <your-ip-address:80>
---><your-ip-address:80/index.php>

### UseCase2:
DevOps team want's to provision a playbook which will create a HIGH AVAILABILITY Application load balancer with nginx
web servers attached to your load balancer.

Your playbook should create the below services:
1) Update Apt packages.
2) Install Haproxy.
3) Backup the original Configuration file.
4) Copy configuration file.
5) Restart Haproxy.
6) Install Nginx server.
7) Copy index.html file in nginx root directory.
8) Restart nginx server.

#### Description
Devops team will work on High availabilty of application,for this they want 
setup Haproxy and nginx environments to test changes in configuration and to make sure that applciation 
is accessed and highly available by load balancer.
For this we develop a playbook to setup the environments which will install HAPROXY and install nginx webserver
and this will be used to check if the applciation is highly available or not.
### Prerequisites:
1) Ansible server.
2) One server for Load balancer.
3) Two servers for nginx web servers.
### How to run the Ansible-playbook:
--> ansible-playbook playbook.yml
### How to access application on browser:
Goto to browser and Enter the Ip address of Loadbalacer.
--> <your-loadbalancer-ip:80/index.html>

### To check high availabilty shutdown one nginx server and access on browser
loadbalancer ip.
<--your-loadbalancer-ip:80/index.html-->
Still you can access the Applicaiton!!!

### UseCase3:
Developers/Devops teams require some basic tools which should be provisioned for testing purpose.
This playbook will helps you install basic tools which are used for CI/CD implementation.

Your playbook should create the below services:
1) Install Git.
2) Install packages.
3) Install wget.
4) Install java 1.8.
5) Install Jenkins.
6) Enable Jenkins.
7) Display the Jenkins initialAdminPassword.
8) Install prerequisites for docker.
9) Install docker.
#### Description
Developers/Devops team requires a set of minimal tool to work on CICD implementaion.
This playbook will help them to provision git,jenkins and docker.
We require these setup mostly in the development phase.This playbook consists of 3 roles,
if we need any other tool then same can be added in the roles directory and we can include
the role in playbook.
### Prerequisites:
1) Ansible server.
2) Host servers.
### How to run the Ansible-playbook:
--> ansible-playbook playbook.yml
### How to check the services running/installed:
1) Login to Host server
--> ssh -i "xyz.pem" ubuntu@host-ip-address
2) Check for git version
--> Git --version
3) Check for jenkins status
--> systemctl status jenkins
4) Check for docker status
--> systemctl status docker

### UseCase4:
Your Manager asks you to write a playbook will install a WordPress website on top of a LAMP environment 
(Linux, Apache, MySQL and PHP) on an Ubuntu machine.

Your playbook should create the below services:
1) Install Apache.
2) Install lamp packages.
3) Install Php Extensions.
4) Create directory in root.
5) Set up Apache VirtualHost.
6) Enable rewrite module.
7) Enable new site.
8) Disable default Apache site.
9) Install MariaDB server package.
10) Start Mysql Service.
11) Install python Mysql package .
12) Set the root password.
13) Remove the MySQL test database.
14) Creates database for WordPress.
15) Create MySQL user for WordPress.
16) Download and unpack latest WordPress
17) Set ownership
18) Set up wp-config
#### Description
Many of the developers work on temporary Lampstack environments
to deploy there wordpress application and test on servers.
When working on Wordpress applications we need this environment for the development phase.
We have designed playbooks to create the environment as per the requirements.
Before running the playbook, we adjust the variables file with required parameters and run it to create the environment.
This playbook will install a WordPress website on top of a LAMP environment (Linux, Apache, MySQL and PHP) on an Ubuntu machine.
### Prerequisites:
1) Ansible server.
2) Host servers.
### How to run the Ansible-playbook:

### 1. Customize Options

```shell
nano vars/default.yml
```

```yml
---
#System Settings
php_modules: [ 'php-curl', 'php-gd', 'php-mbstring', 'php-xml', 'php-xmlrpc', 'php-soap', 'php-intl', 'php-zip' ]

#MySQL Settings
mysql_root_password: "mysql_root_password"
mysql_db: "wordpress"
mysql_user: "sabear"
mysql_password: "password"

#HTTP Settings
http_host: "your_domain"
http_conf: "your_domain.conf"
http_port: "80"
```

### 2. Run the Playbook

```command
ansible-playbook -l [target] -i [inventory file] -u [remote user] playbook.yml
```

### UseCase5:
Developers/Devops team requires to setup k8s master and slave architecture,manual work
is a lenghty process and there are lot of chances for human error.
In order to avoid human errors and use the same networks for different environments we have 
provisioned a playbook which will setup master/slave architecture.

Your playbook should create the below services:
1) Docker Installation.
2) Enable docker.
3) Install APT Transport HTTPS.
4) Add Kubernetes apt-key for APT repository.
5) Add Kubernetes APT repository.
6) Start mysql server.
7) Install kubelet.
8) Install kubeadm.
9) Install kubectl in master.
10) Start the cluster.
11) create .kube directory.
12) copy admin.conf to user's kube config.
13) Install Pod network.
14) Store join command.
15) Set join command.
16) join cluster.
#### Description
Developers uses customized dockerimages with applciation prerequisites
and these images are are stored in any private dockerhub/Azure container registry.
Same images are used for creating k8s deployments and to create the cluster to pods.
This playbook will help to setup the complete environment with one master and two worker nodes.

### Prerequisites:
1) Ansible server.
2) K8s master instance t2.medium.
3) k8s node servers.
### How to run the Ansible-playbook:
Note: Use the same host file present in the Usecase-5 directory.
### To setup k8s master and slave please select t2.medium instance
ansible-playbook -i hosts main.yml

### How to verify nodes
kubectl get nodes

### Run a sample nginx deployment
kubectl create deployment nginx --image=nginx

### Run a service for the nginx deployment
kubectl expose deploy nginx --port 80 --target-port 80 --type NodePort

### To list the services created
kubectl get services

### To test on browser that everything is working,
http://worker_1_ip:nginx_port or http://worker_2_ip:nginx_port 
through a browser on your local machine. You will see Nginx’s familiar welcome page.

### UseCase6:
A nodejs code is in your github private account and you need to write a playbook to clone the source code
from github and install all prerequisites that are required to run nodejs applciation and store the application data 
in mongodb.

Your playbook should create the below services:
1) Install Git.
2) MongoDB - Import public key.
3) MongoDB - Add repository.
4) MongoDB - Install MongoDB.
5) MongoDB - Running state.
6) Node.js - Get script.
7) Node.js - Set execution permission to script.
8) Node.js - Execute installation script.
9) Node.js - Remove installation script.
10) Node.js - Install Node.js
11) Node.js - Install gulp globally
#### Description
A team of developers working on a node js application from different locations,
these developers requires to deploy the applciation in aws environment and check 
the functionality of there application. Every time a aws instance is spinned up is
Terminated after the work is done to avoid the billing. 
The new modules and new changes to code is stored in github repository,all the developers 
need a instance with all nodejs prerequisites to test the functionality of application. 
Each time a developer needs to test he should make the environment ready so that he can deploy the applciation and test,
this work will be done on a regular basis till the final release.
Setting up environment will take lot of time and hence the developers will not be more focussed
on the quality of code rather than setting up environments.
To avoid doing the same work again and again we will be developing a playbook which will help install npm,source management tool, 
install all dependencies.The only thing developers needs to do is deploy the code and test the functionality. With Ansible things are easy!!
### Prerequisites:
1) Ansible server.
2) Host servers.
### How to run the Ansible-playbook:
--> ansible-playbook playbook.yml
### How to check the services running/installed:
1) Login to Host server
--> ssh -i "xyz.pem" ubuntu@host-ip-address
2) Check for git version
--> Git --version
3) Check for jenkins status
--> systemctl status jenkins
4) Check for nodejs and npm versions
--> node --version
--> npm --version