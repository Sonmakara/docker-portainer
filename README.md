Installing Docker from the Official Repository
Remove any old Docker versions
If you have an older version of Docker installed (from your OS repository), let’s remove it to avoid conflicts:
sudo apt remove docker docker-engine docker.io containerd runc

Update the system and install dependencies
Before adding Docker’s repository, it’s a good idea to ensure your system is up-to-date and has the necessary packages for secure downloads:
```
sudo apt update
sudo apt install ca-certificates curl gnupg lsb-release -y
```
Add Docker’s official GPG key
This step ensures that the packages you install are authentic and come from Docker’s trusted source:
```
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg \
  | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
Add the Docker repository
Now, let’s tell your system where to get the official Docker packages:
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
  $(lsb_release -cs) stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Install Docker Engine, CLI, and plugins
With the repository set up, we can install Docker and its related components:
```
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```
Verify Docker installation
Finally, let’s check that Docker is working correctly by running a test container:
```
sudo docker --version
```

Installing Portainer with docker-compose.yml
Create a directory for Portainer configuration
Let’s keep things organized by creating a dedicated folder for Portainer’s data:
```
mkdir -p  /portainer
cd  /portainer
```
Create the docker-compose.yml file
Open your favorite text editor and create the following file:
```
sudo vim docker-compose.yml
```

Paste the following content into the file:
```
version: "3.9"

services:
portainer:
image: portainer/portainer-ce:latest
container_name: portainer
restart: always
ports:
- "8000:8000"
- "9000:9000"
volumes:
- /var/run/docker.sock:/var/run/docker.sock
- portainer_data:/data

volumes:
portainer_data:
```
Start Portainer
From inside the directory containing the docker-compose.yml file, run:
```
sudo docker compose up -d
```

Access Portainer Web UI
Open your browser and visit:
```
https://<server-ip>:9000
```
When you access it for the first time, you will be prompted to create an admin account. Once logged in, choose Local to connect Portainer to your local Docker environment.
Conclusion
By combining Docker with Portainer, you get a powerful containerization platform paired with an easy-to-use management interface. Installing Docker from the official repository ensures you have the latest stable version and security updates, while deploying Portainer via docker-compose.yml keeps the setup clean and maintainable.<img width="961" height="2542" alt="image" src="https://github.com/user-attachments/assets/1dc6a4f7-4bea-49bd-aac2-cb8a6f111f59" />
