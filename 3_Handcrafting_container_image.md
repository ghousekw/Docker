## Get and Run the Base Image

### 1. Retrieve the httpd image:

    docker pull httpd:2.4

### 2. Run the image:

    docker run --name webtemplate -d httpd:2.4

### 3. Check the status of the webtemplate container:

    docker ps

***


## Install Tools and Code in the Container

### 1. Log in to the container:

    docker exec -it webtemplate bash

### 2. Run apt update and install git

    apt update && apt install git -y

### 3. Clone the website code from GitHub:

    git clone  https://github.com/linuxacademy/content-widget-factory-inc.git /tmp/widget-factory-inc

### 4. Verify that the code was cloned successfully:

    ls -l /tmp/widget-factory-inc/

### 5. List the files in the htdocs/ directory:

    ls -l htdocs/

### 6. Remove the index.html file:

    rm htdocs/index.html

### 7. Copy the webcode from /tmp/ to the htdocs/ folder:

    cp -r /tmp/widget-factory-inc/web/* htdocs/

### 8. Verify that they were copied over successfully:

    ls -l htdocs/

### 9. Exit the container:

    exit

***

## Create an Image from the Container

### 1. Copy the Container ID:

    docker ps

### 2. Create an image from the container:

    docker commit <CONTAINER_ID> example/widgetfactory:v1

### 3. Verify that the image was created successfully:

    docker images

### 4. Take note of the image size. 

***

## Clean up the Template for a Second Version

### 1. Log in to the container:

    docker exec -it webtemplate bash

### 2. Remove the cloned code from the /tmp/ directory:

    rm -rf /tmp/widget-factory-inc/

### 3. Use apt to uninstall git and clean the cache:

    apt remove git -y && apt autoremove -y && apt clean 

### 4. Exit the container:

    exit

### 5. Check the status of the container:

    docker ps

### 6. Create an image from the updated container:

    docker commit <CONTAINER_ID> example/widgetfactory:v2

### 7. Verify that both images are now running:

    docker images  

### 8. Delete the v1 image:

    docker rmi example/widgetfactory:v1

***

## Run Multiple Containers from the Image

### 1. Run multiple containers using the new image:

    docker run -d --name web1 -p 8081:80 example/widgetfactory:v2
    docker run -d --name web2 -p 8082:80 example/widgetfactory:v2
    docker run -d --name web3 -p 8083:80 example/widgetfactory:v2

### 2. Check the status of the containers:

    docker ps

### 3. Stop the base webtemplate image:

    docker stop webtemplate

### 4. Verify that only the created containers are running:

    docker ps

### 5. Using a web browser, verify that the containers are running successfully:

    <SERVER_PUBLIC_IP_ADDRESS>:8081
    <SERVER_PUBLIC_IP_ADDRESS>:8082
    <SERVER_PUBLIC_IP_ADDRESS>:8083