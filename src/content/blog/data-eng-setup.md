---
author: Ash
pubDatetime: 2025-06-22T7:20:00Z
title: My Minimal Data Engineering Setup
postSlug: My-Minimal-Data-Engineering-Setup
featured: true
draft: false
tags:
  - data-engineering
ogImage: ""
description: My Minimal Data Engineering Setup on Linux
---

🛠️ My Minimal Data Engineering Setup (Linux Mint)

Set up Docker, Microsoft SQL Server, and DBeaver Community Edition, superset,postgres on Linux Mint for a local data engineering environment — all in one place.

---

## 📦 Install Docker

Update and install prerequisites:

```bash
sudo apt update
sudo apt install ca-certificates curl gnupg lsb-release
```

Add Docker’s GPG key:

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

Add the Docker repository for Ubuntu Jammy (works on Linux Mint 21+):

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu jammy stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Install Docker:

```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Enable and start Docker:

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

(Optional) Allow current user to run Docker without `sudo`:

```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

## 🐘 Run Microsoft SQL Server in Docker

Create and run the container:

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyNewStrong@123" \
  -p 1433:1433 --name mssql \
  -d mcr.microsoft.com/mssql/server:2022-latest
```

> ⚠️ Replace `MyNewStrong@123` with a strong password (min 8 chars, uppercase, lowercase, number, special character).

Verify container is running:

```bash
docker ps
```

---

## 🧪 (Optional) Install `sqlcmd` CLI for Command-Line Access

Import Microsoft repo and install tools:

```bash
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/ubuntu/22.04/prod jammy main" > /etc/apt/sources.list.d/msprod.list'
sudo apt update
sudo apt install mssql-tools unixodbc-dev
```

(Optional) Add `sqlcmd` to your shell path:

```bash
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
```

Test connection:

```bash
/opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P 'MyNewStrong@123'
```

Inside the prompt, test with:

```sql
SELECT @@VERSION;
GO
```

---

## 🦫 Install DBeaver Community Edition

### Option 1: Download and install `.deb` package

```bash
wget https://dbeaver.io/files/dbeaver-ce_latest_amd64.deb
sudo apt install ./dbeaver-ce_latest_amd64.deb
```

### Option 2: Install via Flatpak

```bash
flatpak install flathub io.dbeaver.DBeaverCommunity
```

Launch from your application menu after install.

---

## 🔗 Connect to SQL Server via DBeaver

1. Open DBeaver
2. Click **New Database Connection**
3. Choose **SQL Server**
4. Fill in:

   - Host: `localhost`
   - Port: `1433`
   - Username: `sa`
   - Password: `MyNewStrong@123`

5. Click **Test Connection**
6. Click **Finish**

---

## 💾 Optional: Use Docker Volume for Data Persistence

If you want your SQL Server data to persist even after deleting the container:

```bash
docker rm -f mssql
docker volume create mssql_data
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyNewStrong@123" \
  -p 1433:1433 --name mssql \
  -v mssql_data:/var/opt/mssql \
  -d mcr.microsoft.com/mssql/server:2022-latest
```

## 💾 Postgress via docker

Create and run the postgress container:

```bash
docker run --name postgres \
  -e POSTGRES_USER=rootp\
  -e POSTGRES_PASSWORD=MyNewStrong@123\
  -e POSTGRES_DB=mydb \
  -p 5432:5432 \
  -v pg_data:/var/lib/postgresql/data \
  -d postgres:15
```

To start postgres container in docker:

`docker start postgres`

## Installing superset

```
    git clone https://github.com/apache/superset.git

    sudo apt install docker-compose

    docker compose -f compose-non-dev.yml up
```

Open http://localhost:8088
