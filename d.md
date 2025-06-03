# Docker Basics: Step-by-Step Guide

## 1️⃣ Installation & Verification
```bash
docker --version          # Check Docker installation
docker info               # Display system-wide information

2️⃣ Image Management
bash
docker images             # List all local images
docker rmi <image_id>     # Remove an image
docker pull nginx         # Download an image from Docker Hub
docker image history <image_name>  # Show image layer history

3️⃣ Building Custom Images
bash
docker build -t myapp:1.0 .   # Build an image from Dockerfile 
docker tag myapp:1.0 username/myapp:1.0   # Tag an image for Docker Hub

4️⃣ Container Operations
bash
docker run -p 8080:80 myapp:1.0  # Run a container with port mapping
docker run -it --rm busybox bash  # Run interactively + auto-remove

✅ Manage containers 
docker ps -a --format "table {{.ID}}\t{{.Names}}\t{{.Status}}"  # Custom format
docker stop <container_id>
docker start <container_id>
docker rm <container_id>        # Delete a stopped container
docker top <container_name>     # View running processes

✅ Stop/Remove all containers
docker stop $(docker ps -aq)
docker rm $(docker ps -aq)

5️⃣ Docker Hub Integration
bash
docker login              # Authenticate to Docker Hub
docker push username/myapp:1.0  # Upload image
docker pull username/myapp:1.0  # Download image

🛠️ Common Solutions
Fix: Run a New Interactive Container That Stays Alive
bash
docker run -it ubuntu bash

✅ Basic Container Setup
bash
docker build -t my-project-image .   # Build the Docker Image
docker run -it -p 3000:3000 my-project-image   # Run the Container

🔄 Docker Image Transfer Guide (Without Remote Registry)
Copy Docker images between servers without Docker Hub or a private repository.

1️⃣ Export the Docker Image (Source Server)
bash
docker images
docker save -o /path/to/image.tar image_name:tag

2️⃣ Transfer the .tar File
bash
# Using rsync (recommended)
rsync -avz /path/to/image.tar user@destination_ip:/path/to/destination/

✅ Alternative: SCP
scp /path/to/image.tar user@destination_ip:/path/to/destination/

3️⃣ Import the Docker Image (Destination Server)
bash
docker load -i /path/to/image.tar
docker images

🔍 Verification
bash
docker images | grep <image_name>

💡 Tips
bash
# Compress large images
gzip /path/to/image.tar
rsync -avz image.tar.gz user@destination_ip:/path/
gunzip image.tar.gz     # On destination server

📊 Monitoring
bash
docker stats    # Live container resource usage

----------------------------
✅ To run the basic website in local
sudo docker pull httpd   # To pull the image from docker hub
sudo docker run -d --name webserver -p 9090:80 httpd  # to run the webserver from localhost 9090
udo docker ps -a # to check it whther port transfer the data
output :
      NAMES
b5e22fe312ab   httpd               "httpd-foreground"       16 seconds ago   Up 15 seconds               0.0.0.0:9090->80/tcp, :::9090->80/tcp

------------------------------------------------
sudo docker start <image_name>  # Start container or image 
sudo docker exec -it <image_name> bash    # Entering to webserver image
htdocs  # (HyperText Documents) is Apache's default directory for serving web files

root@b5e22fe312ab:/usr/local/apache2/htdocs# ls index.html  #

sudo docker diff <image /id>  # Shows filesystem changes in a container
sudo docker commit <image /id> # Creates new image from container's changes
sudo docker start webserver   # To start a container
sudo docker stop <image>    # to stop a container
sudo docker login
---------------------------------------------------------------------
'sudo docker run -d --name myownserver -p 5070:80 b5e22fe312ab'

docker run
    The base command to create and start a new Docker container

-d (detach)
    Runs the container in background (daemon mode) instead of attaching to your terminal

--name myownserver
    Assigns a custom name (myownserver) to the container for easier management
    Without this, Docker would generate a random name

-p 5070:80 (port mapping)
    Maps port 5070 on your host machine to port 80 inside the container
    Format: -p <host-port>:<container-port>
    This allows accessing the containers service at http://localhost:5070

b5e22fe312ab <image id>
      The problematic part - this should be either:
      A valid image name (like nginx:latest)
---------------------------------------------------------------
File transfer through local Like pen drive

' docker load -i myhttpd-v1.tar ' # Transferring images between machines without a registry (e.g., air-gapped systems).

-------------------------------------------------------------------
After 'pull' from docker hub

# 1. Run the container
sudo docker run -d -p 8080:80 --name my_httpd prem25/myhttpd:v1

      Command Structure: Part	Explanation
'sudo'	            Executes the command with root privileges (required unless your user is in the docker group)
'docker run'	      The base command to create and start a new container from an image
'-d'	                  Detached mode: Runs the container in the background
'-p 8080:80'	      Port mapping: Binds host port 8080 to container port 80
'--name my_httpd'	      Assigns a custom name (my_httpd) to the container
'prem25/myhttpd:v1'     The image to use (format: [username]/[repository]:[tag])
 

# 2. Verify it's running
sudo docker ps

# 3. Test access
curl localhost:8080

# 4. Stop when needed
sudo docker stop my_httpd

# 5. Remove when finished
sudo docker rm my_httpd
