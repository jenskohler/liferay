# Building the container

The following VM is the foundation for the Docker installation:
- Basic OS: Debian 8 Server
- Docker Version: 17

# Install Docker

    sudo apt-get update
 
    sudo apt-get install \
         apt-transport-https \
         ca-certificates \
         curl \
         gnupg2 \
         software-properties-common
 
    curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | sudo apt-key add -
 
    sudo apt-key fingerprint 0EBFCD88
 
    sudo add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
       $(lsb_release -cs) \
       stable"
 
    sudo apt-get update
    sudo apt-get install docker-ce
 
    sudo docker run hello-world
 
    sudo groupadd docker
 
    sudo usermod -aG docker $USER
 
    docker run hello-world
 
    sudo systemctl enable docker
    
# Create a Docker Swarm

    docker swarm init
    
    docker stack deploy -c liferay-stack.yml liferay-stack
    

# Useful Docker commands

Remove all containers
      
    docker rm $(docker ps -aq)
      
Remove all images

    docker rmi $(docker images -q)    
    
Commit changes done in a container to create a new image layer

    docker commit -m "<commit message>" -a "<author-name>" <container-id> <repositrory>/<new-image-id>
    
Push a new image to a repository

    docker login -u <user-name>
    
    docker push <author-name>/<new-image-id>
    
# Basic images for the created Dockerfiles
An initial Liferay installation was done based on the following image

    docker pull liferay/portal:7.1.0-ga1-201809012030
    
    docker run -it -p8080:8080 liferay/portal:7.1.0-ga1-201809012030 -v/home/jens/liferay:/etc/liferay/mount  
    
The concrete installation steps can be found in [liferay7_installation_steps.pdf](liferay7_installation_steps.pdf) 

An initial MariaDB installation was done base on the following image

     docker run -it --link my_mariadb -v ${PWD}/persistent/webapps:/usr/local/tomcat/webapps -p8080:8080 -p8005:8005 -p8009:8009 finde/tomcat8-liferay7
        
       