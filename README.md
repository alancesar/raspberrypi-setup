# About
This project contains the setup needed to configure my personal Raspberry Pi environment.

# Dependencies

## Installing OpenMediaVault (OMV)
Update the packages and Raspberry Pi EEPROM:
```shell
sudo apt update && sudo apt full-upgrade
```

Run the OMV installation script:
```shell
wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash
```

## Installing Tailscale
Run the command below:

```shell
curl -fsSL https://tailscale.com/install.sh | sh
```

## Installing Docker
Run the command below to execute the one-line installer. Read more about [here](https://github.com/docker/docker-install).

```shell
curl -sSL https://get.docker.com/ | sh
```

Add your user to `docker` group:

```shell
sudo groupadd docker
sudo usermod -aG docker $USER
```

## Running Portainer
Portainer is a graphical interface for managing Docker containers.
Start the Portainer with the command bellow or just running `./start-portainer.sh`.

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

- `APPS`: the path for applications file and configurations;
- `DATA`: the downloads and media root path;
- `USERNAME`: default username for services;
- `PASSWORD`: default password for services.

Example:
```plaintext
APPS=/path/to/apps
DATA=/path/to/media
USERNAME=default_user
PASSWORD=default_pass
```

The environment contains:
- [Homepage](https://gethomepage.dev/): A dashboard with utilities and links for the services.
- [Postgres](https://www.postgresql.org/): Open source relational database.
- [pgAdmin](https://www.pgadmin.org/): Graphical interface for Postgres.
- [RabbitMQ](https://www.rabbitmq.com/): Queue service.
- [AdGuard Home](https://adguard.com/pt_br/adguard-home/overview.html): DNS server with ads blocker.
- [Plex](https://www.plex.tv/pt-br/): Personal media streaming service. It uses the [linuxserver.io](https://hub.docker.com/r/linuxserver/plex) image.
- [Transmission](https://transmissionbt.com/): A BitTorrent client. It uses the [linuxserver.io](https://hub.docker.com/r/linuxserver/transmission) image.

# Running
Access the home at http://<<raspberrypi-address>>