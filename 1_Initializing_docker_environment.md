## Installing Docker on CentOS/Fedora machine:
### 1. Install the Docker prerequisites:

    sudo yum install -y yum-utils device-mapper-persistent-data lvm2


Using yum-config-manager, add the CentOS-specific Docker repo:
    
    sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

### 2. Install Docker:

    sudo yum -y install docker-ce

### 3. Enable the Docker Daemon:

    sudo systemctl enable --now docker


## Configure User Permissions

### 1. Add the lab user to the docker group:

    sudo usermod -aG docker cloud_user

> Note: You will need to exit the server for the change to take effect. 

### 2. Run a Test Image

 Using docker, run the hello-world image to verify that the environment is set up properly:

    docker run hello-world
