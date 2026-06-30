# 🌐 Custom Production Nginx Gateway

This folder contains a custom-built, enterprise-ready Nginx image designed for container orchestration networks. It handles log rotation, automatic self-signed SSL fallback, and dynamic site mounting.

---

## 🧩 How It Works

This setup relies on **two phases**: a custom image build layer and an orchestration deployment layer.

### 1. The Build Phase (`Dockerfile`)
Instead of using a stock image, we compile a secure environment based on `nginx:alpine`:
* **Security:** Runs under an isolated `www-data` system user.
* **Log Maintenance:** Bundles `logrotate` via a background cron daemon to stop log files from filling up the disk.

### 2. The Boot Phase (`startup.sh`)
When the container turns on, it runs an initialization lifecycle script:
1. Checks for a certificate in `/etc/nginx/ssl/`. If empty, it creates a fallback **self-signed SSL certificate** (`default.crt`) instantly so the engine starts without errors.
2. Starts the background Cron agent for log recycling.
3. Fires up the Nginx server in the foreground.

---

## 📁 Mount Points & Folder Structure

When deployed via `docker-compose_deploy.yml`, your host machine folders map into the container like this:

* **`./ssl/`** ➡️ `/etc/nginx/ssl/` — Stores your active SSL/TLS domain certificates.
* **`${CONF_PATH}/sites`** ➡️ `/etc/nginx/sites` — Where you drop your reverse proxy domain configurations.
* **`${CONF_PATH}/conf.d`** ➡️ `/etc/nginx/conf.d` — For global Nginx optimization fragments.
* **`${LOG_PATH}`** ➡️ `/var/log/nginx` — Maps container transaction files back to the host for streaming or backup.

---

## 🚀 Deployment

1. Set up your active configurations inside your host directory paths.
2. Make your execution pipeline tool ready:
   ```bash
   chmod +x build-deploy
   ./build-deploy
