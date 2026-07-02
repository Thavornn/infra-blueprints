# GitLab 

This project deploys GitLab Community Edition (CE) as a Docker Swarm stack. The deployment is configured through environment variables, making it easy to customize the GitLab URL and other settings without modifying the stack files.

---

## Quick Start 

1. **Configure Environment:**
   ```bash
   cp env.example .env
   ```
   Open .env and set your server's real IP or domain in GITLAB_EXTERNAL_URL
2. **Deploy the Stack:**
    ```bash
    sudo ./deploy.sh
    ```
3. **Monitor the process**:
    GitLab takes 3-5 minutes to fully initialize. Check it status with:
    ```bash
    sudo docker service logs -f gitlab_gitlab
    ```
4. **Get the Initial Admin Password:**
    After Gitlab starts, retrieve the temporary **root** Password by running:
    ```bash 
    sudo cat /var/data/gitlab/config/initial_root_password
    ```
    Use this password to sign in to GitLab as the **root** user.
    > **Important:** This file is automatically deleted after 24 hours. Log in as soon as possible and change the root password immediately.

