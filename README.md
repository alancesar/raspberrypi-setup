# About
This script contains the setup needed to configure my personal Raspberry Pi environment.

# Dependencies

## Installing OpenMediaVault
Update the packages and Raspberry Pi EEPROM:
```shell
sudo apt update && sudo apt full-upgrade
```

Run the OMV installation script:
```shell
wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash
```

## Installing Docker
Read more about [here](https://github.com/docker/docker-install).

```shell
curl -sSL https://get.docker.com/ | sh
```

## Running Portainer
Start the Portainer with the command bellow or just running `./start-portainer.sh`

```shell
docker volume create portainer_data &&
docker run --name portainer \
    -p 8000:8000 \
    -p 9443:9443 \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    -d portainer/portainer-ce:2.21.5
```

# Setup Portainer
The `docker-compose.yaml` contains the setup for all the services. Just fill the `.env` with this data:

- `APPS`: the path for applications file and configurations
- `DATA`: the downloads and media root path
- `USERNAME`: default username for services
- `PASSWORD`: default password for services

The environment contains:
- [Homepage](https://gethomepage.dev/): A dashboard with utilities and links for the services.
- [Postgres](https://www.postgresql.org/): Open source relational database.
- [pgAdmin](): Graphical interface for Postgres.
- [RabbitMQ](https://www.pgadmin.org/): Queue service.
- [AdGuard Home](https://adguard.com/pt_br/adguard-home/overview.html): DNS server with ads blocker.
- [Plex](https://www.plex.tv/pt-br/): Streaming service. It uses the [linuxserver.io](https://hub.docker.com/r/linuxserver/plex) image.
- [Transmission](https://transmissionbt.com/): A BitTorrent client. It uses the [linuxserver.io](https://hub.docker.com/r/linuxserver/transmission) image.