# MongoDB Provision(Ubuntu 24.04)
Tells Linux that it's running a bash script
`#! /bin/bash`

Checks for updates on available  packages and upgrades them

```bash
sudo apt update -y
sudo apt upgrade -y
```

Imports MongoDB public GPG key

```bash 
curl -fsSL https://pgp.mongodb.com/server-8.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
   --dearmor
```

Creates a List file with a web address on where to install MongoDB 8.2

```bash
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.2.list
```

Reloads the local package database

```bash
sudo apt-get update -y
```

Installs MongoDB 8.2.5 and related components of the same version

```bash
sudo apt-get install -y \
   mongodb-org=8.2.5 \
   mongodb-org-database=8.2.5 \
   mongodb-org-server=8.2.5 \
   mongodb-mongosh \
   mongodb-org-shell=8.2.5 \
   mongodb-org-mongos=8.2.5 \
   mongodb-org-tools=8.2.5 \
   mongodb-org-database-tools-extra=8.2.5
```

Checks if MongoDB is running and detected, then starts MongoDB, then adds it to system boot so it starts automatically when the machine is run

```bash
sudo systemctl status mongod
sudo systemctl start mongod
sudo systemctl enable mongod
```
