# Step 1: Install Docker
Open your Raspberry Pi terminal and run these commands to install Docker and Docker Compose.

A. Download and install Docker
```curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

B. Add your user to the docker group
```
sudo usermod -aG docker $USER (Change this with your username)
```

C. Reboot

# Step 2: Install Home Assistant

A. Create a folder for your project
```
mkdir ~/homeassistant
cd ~/homeassistant
```
B. Create a compose.yaml file
```
nano compose.yaml
```
C. Paste this configuration
```
services:
  homeassistant:
    container_name: homeassistant
    image: "ghcr.io/home-assistant/home-assistant:stable"
    platform: linux/arm64
    volumes:
      - ./config:/config
      - /etc/localtime:/etc/localtime:ro
    restart: unless-stopped
    privileged: true
    network_mode: host
```
D. Start Home Assistant
```
docker compose up -d
```
# Step 3: You can now access your dashboard at http://localhost:8123
