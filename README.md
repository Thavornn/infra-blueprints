# Infra Blueprints
 This repository is a collection of pre-configured, self-contained service templates ready to be deployed instantly.

Think of this repo as a LEGO box for server infrastructure. Instead of manually installing and configuring databases, web servers, message queues, and other services every time, each component is packaged as a modular, containerized stack using Docker Swarm and Podman—with a structure that's easy to extend to Kubernetes (K8s) or other orchestration and automation tools in the future.

### 📁 How it's structured:
* **Root Level (`/`):** Contains system initialization scripts (like `init-swarm.sh`) to prepare a fresh Linux machine.
* **Subfolders (e.g., `postgres/`, `nginx/`):** Each tool has its own dedicated folder. Inside each folder, you will find its `docker-compose.yml`, environment configuration files, and a **local README** explaining how to run that specific tool.

---

##  Quick Start: How to use it

If you just cloned this repo onto a fresh Linux machine, follow these steps:

### 1. Initialize Docker & Swarm
Prepare your host machine by running the setup script from the root folder:
```bash
# Grant execution permissions to the core initializer
chmod +x init-swarm.sh

# Run the script to configure GPG keys, repository mirrors, runtimes, and Swarm states
./init-swarm.sh
```
---
### 2. Deploy a Tool

Pick a tool you want to run, navigate to its folder, and follow its local guide:
```bash
cd postgres/
cp env.example .env   # Set up your local passwords
```
you have 2 way to deploy the tool
#### Option 1: Docker Swarm 
```bash
chmod +x deploy.sh
./deploy.sh
```
#### Option 2: Docker Compose 
```bash
docker compose up -d    # Standard Docker Compose
```

## Ideas: What can you do with this repo

This repo is built to grow. Here is what you can do with this structure as you learn or build new things:

- **Spin up dev environments instantly:** Need a quick database for a project? Just jump into `postgres/` or `redis/` and launch it.
- **Plug in new tools easily:** Learned a new tool (like Prometheus or Grafana)? Just create a new folder, drop a `docker-compose.yml` in it, and your ecosystem expands.
- **Upgrade to new technologies:** If you move from Docker Swarm to Kubernetes or Ansible in the future, you can just add a `k8s/` or `ansible/` folder right here without changing the structure.

```

