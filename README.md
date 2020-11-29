Prerequisites
Before you can run a deployment, you’ll need the following installed in your local environment:
•	Ansible Requires Version 2.8+
•	Docker
•	A recent version
•	docker Python module
•	This is incompatible with docker-py. If you have previously installed docker-py, please uninstall it.
•	We use this module instead of docker-py because it is what the docker-compose Python module requires.
•	Git Requires Version 1.8.4+
•	Python 3.6+
System Requirements
The system that runs the WIKIMEDIA service will need to satisfy the following requirements
•	At least 4GB of memory
•	At least 2 cpu cores
•	At least 20GB of space
•	Running Docker, Kubernetes
Installation steps:
1. Install Dependencies
yum install -y epel-release
yum remove python-docker-py
yum install -y yum-utils device-mapper-persistent-data lvm2 ansible git python-devel python-pip python-docker-py vim-enhanced
pip install cryptography
pip install jsonschema
pip install docker-compose~=1.23.0
pip install docker –upgrade
2. Install docker
Configure docker ce stable repository.
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
Installing docker.
yum install docker-ce -y
Start docker service.
systemctl start docker
Enable docker service.
systemctl enable docker
3. Deploy WIKIMEDIA
Clone WIKIMEDIA repo
git clone https://github.com/dipchavan/wikimedia.git

Configure WIKIMEDIA
Add required hosts in the “inventory” file.

Deploy WIKIMEDIA
•	cd wikimedia/installer
•	ansible-playbook -i inventory deploy.yml -vv

Check the status
docker ps -a

You will see the images built like this form Dockerfiles:

 

WIKIMEDIA is ready and can be accessed from the browser.
http://ipaddress:80/
the default username is “admin” and the password is “password”.
Final checks:
1.	verify whether the service is started or not with ss -tlnp | grep 80
2.	make sure your firewall is open for port 80
3.	make sure your OS is using python 3.6+ and pip3


