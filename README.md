<p align="center">
  <img width="100" height="100" src="https://user-images.githubusercontent.com/63885192/177281052-4a89a5aa-232a-4276-b22d-9e7dc0cb9334.png">
</p>

# Tutorial Run SubQuery Public Testnet (Phase 3)

Source: https://academy.subquery.network/subquery_network/testnet/indexers/index-project.html

## Recommended Hardware Requirements

* 4 vCPU Cores
* 8 GB RAM
* 200 GB SSD
* 32 TB Traffic
* Location: Nuremberg/bebas
* OS: Ubuntu 21.10 (64 Bit)

## Update packages & Install required packages

```
sudo apt update && sudo apt upgrade -y
```
```
sudo apt install wget jq build-essential nano unzip -y
```
## Install Docker

```
. <(wget -qO- https://raw.githubusercontent.com/SecorD0/utils/main/installers/docker.sh)
```
## Enable Firewall

```
sudo apt install ufw -y
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 8000
sudo ufw allow 9090
sudo ufw allow 9100
sudo ufw allow 3000:3100/tcp
```
## Clone repository

```
mkdir subquery-indexer
curl https://raw.githubusercontent.com/subquery/indexer-services/main/docker-compose.yml -o $HOME/subquery-indexer/docker-compose.yml
```
## Create service file

```
printf "[Unit]
Description=Subquery systemd service
After=network.target
StartLimitIntervalSec=0

[Service]
User=$USER
Type=simple
Restart=on-failure
RestartSec=10
User=root
SyslogIdentifier=subquery
SyslogFacility=local7
KillSignal=SIGHUP
WorkingDirectory=$HOME/subquery-indexer
ExecStart=`which docker-compose` up -d

[Install]
WantedBy=multi-user.target" > /etc/systemd/system/subquery.service
```
## ⠀Launch service

```
systemctl enable subquery.service 
systemctl start subquery.service 
systemctl status subquery.service
```
## wait 2 minutes and check the containers
```
docker ps
```
![Screenshot_38](https://user-images.githubusercontent.com/63885192/177284935-d4ffd6a7-65fc-4c16-afe4-79ffe7b2d2b4.png)

#### Access your vps IP in browser with additional 8000 ports example http://127.0.0.1:8000

![Screenshot_39](https://user-images.githubusercontent.com/63885192/177285723-fc1315b2-51bd-419f-b1cd-8844f386d48e.png)

#### And complete missions to receive points here https://frontier.subquery.network/missions/my-missions
