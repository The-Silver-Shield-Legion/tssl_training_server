# ☀ TSSL Bannerlord Server
TSSL is a customizable Bannerlord server setup that allows you to quickly deploy a dedicated server using Docker. This guide provides instructions for setting up the server on both local and remote machines, as well as automating the build and deployment process using GitHub Actions.

---

## 🏠 Local Server Setup

#### 1. Clone Repository
`git clone https://github.com/vojinpavlovic/tssl`

#### 2. Install Docker 
- [Linux Debian](https://docs.docker.com/engine/install/debian/)
- [Windows](https://docs.docker.com/desktop/setup/install/windows-install/) 

#### 3. Build Docker Image
`docker build -t blsrv .`

#### 4. Run Docker Image
`docker run -d --name {{server_name}} -p 7210:7210/tcp -p 7210:7210/udp blsrv`

**Note:** Replace `{{server_name}}` with proper name e.g `tssl_sample_srv`

---

## 🌐 Remote Server Setup (Linux Debian)

#### 1. Install Docker
- Update the Package Index: 
``` 
sudo apt-get update 
```

- Install Required Dependencies:
``` 
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
```

- Add Docker’s Official GPG Key:
```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

- Set up the Stable Docker Repository:
```
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

- Update the Package Index Again:
```
sudo apt-get update
```

- Install Docker Engine:
```
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

- Verify Installation
```
sudo docker --version
```

- Add user to Docker Group
```
sudo usermod -aG docker $USER
```

- Verify Docker without Sudo
```
docker ps
```

---

## 🔐 Github Stored Secrets

Secrets are stored in [Actions secrets and variables](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions) on GitHub.

In order to enable deployment workflow you need [Docker Hub](https://hub.docker.com) account.

**Docker Hub**
- DOCKER_USERNAME `Docker Username for docker repository access`
- DOCKER_PASSWORD `Docker Password for docker repository access`

**Secrets for Deployment (SSH)**
- BL_SRV_TOKEN: `Generated TW token from Console Commands`
- REMOTE_SERVER_IP: `IPv4`
- REMOTE_SERVER_USER `Linux User`
- REMOTE_SSH_KEY `SSH key for Remote Access`

---

## 🚀 Github Actions
- [Build](https://github.com/vojinpavlovic/tssl/actions/workflows/deploy.yml) `Manual Execution`
Builds the latest Docker image from the [dockerfile](https://github.com/vojinpavlovic/tssl/blob/main/dockerfile) and pushes it to Docker Hub

- [Deploy](https://github.com/vojinpavlovic/tssl/actions/workflows/deploy.yml) `Manual Execution`
Deploys a container on the Training Server (remote server) using the latest image from Docker Hub.

---

## 🧾 License

This project is licensed under the **MIT** License. See the [LICENSE](https://github.com/vojinpavlovic/tssl/blob/main/LICENSE) file for more details.
