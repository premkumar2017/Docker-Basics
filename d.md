
markdown
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
# Build an image from Dockerfile 
docker build -t myapp:1.0 .  

# Tag an image for Docker Hub 
docker tag myapp:1.0 username/myapp:1.0
4️⃣ Container Operations
bash
# Run a container with port mapping 
docker run -p 8080:80 myapp:1.0  

# Run interactively + auto-remove
docker run -it --rm busybox bash

# Manage containers 
docker ps -a --format "table {{.ID}}\t{{.Names}}\t{{.Status}}"  # Custom format
docker stop <container_id>
docker start <container_id>
docker rm <container_id>        # Delete a stopped container
docker top <container_name>     # View running processes

# Stop/Remove all containers
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
Basic Container Setup
bash
# Build the Docker Image
docker build -t my-project-image .

# Run the Container
docker run -it -p 3000:3000 my-project-image
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

# Alternative: SCP
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
This guide covers Docker basics from installation to advanced container management and image transfer.

