# AI Agent Tools Docker Setup

## Prerequisites

- Docker installed

## Setup

### Fix Docker permissions on Linux (one-time)

```bash
sudo usermod -aG docker $USER
newgrp docker
```

### Run LangFlow locally

```bash
docker run -d --name langflow --restart unless-stopped \
    -p 7860:7860 \
    -v langflow_data:/root/.langflow \
    langflowai/langflow:latest
```

LangFlow will be available at **http://localhost:7860**

### Run LangFlow on a workstation

```bash
docker run -d --name langflow --restart unless-stopped \
    -p 0.0.0.0:7860:7860 \
    -v langflow_data:/root/.langflow \
    langflowai/langflow:latest
```

### Run n8n locally

```bash
docker run -d --name n8n --restart unless-stopped \
    -p 5678:5678 \
    -v n8n_data:/home/node/.n8n \
    docker.n8n.io/n8nio/n8n
```

n8n will be available at **http://localhost:5678**

### Run n8n on a workstation

```bash
docker run -d --name n8n --restart unless-stopped \
    -p 0.0.0.0:5678:5678 \
    -e N8N_LISTEN_ADDRESS=0.0.0.0 \
    -e N8N_SECURE_COOKIE=false \
    -v n8n_data:/home/node/.n8n \
    docker.n8n.io/n8nio/n8n
```

### Run Flowise AI locally

```bash
docker run -d --name flowise --restart unless-stopped \
    -p 3000:3000 \
    -v flowise_data:/root/.flowise \
    flowiseai/flowise:latest
```

Flowise AI will be available at **http://localhost:3000**

### Run Flowise AI on a workstation

```bash
docker run -d --name flowise --restart unless-stopped \
    -p 0.0.0.0:3000:3000 \
    -v flowise_data:/root/.flowise \
    flowiseai/flowise:latest
```

## Useful Commands

```bash
# Check running containers
docker ps

# Check all containers (including stopped)
docker ps -a

# Start/Stop n8n
docker start n8n
docker stop n8n

# Restart n8n
docker restart n8n

# Start/Stop Flowise AI
docker start flowise
docker stop flowise

# Restart Flowise AI
docker restart flowise

# Start/Stop LangFlow
docker start langflow
docker stop langflow

# Restart LangFlow
docker restart langflow

# View logs
docker logs -f n8n
docker logs -f flowise
docker logs -f langflow

# Inspect container details (IP, mounts, env vars, etc.)
docker inspect n8n
docker inspect flowise
docker inspect langflow

# Check resource usage (CPU, memory)
docker stats n8n flowise langflow

# Open a shell inside the container
docker exec -it n8n sh
docker exec -it flowise sh
docker exec -it langflow sh

# Remove container (data is preserved in the volume)
docker rm -f n8n
docker rm -f flowise
docker rm -f langflow

# List volumes
docker volume ls

# Remove the data volumes (WARNING: deletes all data)
docker volume rm n8n_data
docker volume rm flowise_data
docker volume rm langflow_data
```
