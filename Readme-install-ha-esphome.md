### Install Docker, Home Assistant Core and ESP Home:
```
sudo apt-get install -y jq wget curl avahi-daemon udisks2 libglib2.0-bin network-manager dbus docker-compose  
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
sudo service docker start
```

### Make dirs and create Docker Compose file:
```
mkdir /apps/ha -p
mkdir /apps/tw 
cd /apps/ha
nano ./docker-compose.yml
```

### Paste this yaml into the docker-compose.yml file:

```
version: '3'
services:
  homeassistant:
    container_name: homeassistant
    image: "ghcr.io/home-assistant/home-assistant:stable"
    volumes:
      - /apps/ha/config:/config
      - /etc/localtime:/etc/localtime:ro
    restart: unless-stopped
    privileged: true
    network_mode: host
  esphome:
    container_name: esphome
    image: ghcr.io/esphome/esphome
    volumes:
      - /apps/ha/esphome/config:/config
      - /etc/localtime:/etc/localtime:ro
    restart: always
    privileged: true
    devices:
      - /dev/ttyUSB0:/dev/ttyACM0
#   network_mode: host
    ports:
      - 80:6052
```
* Remove the `esphome` codeblock if you only need Home Assistant Core
* Change port 80 to port you want to use for ESPHome Dashboard or remove the "ports" code block and uncomment network_mode: host to use default port of 6052
* Then run docker compose    

`docker compose up -d`

some debian system might need:

`sudo docker-compose up -d`

### Start ESPHome daskboard on demand: 

If there is no device at location `/dev/ttyUSB0` then the docker container will not start automatically and you must use the command below to start the container once you have connected your device. 

Start without USB:
`docker run --rm --net=host -v "${PWD}":/config -it ghcr.io/esphome/esphome`

Start with USB:
`docker run --device=/dev/ttyUSB0 --rm --net=host -v "${PWD}":/config -it ghcr.io/esphome/esphome`

### Upgrade ESPHome and HomeAssistant containers: 

```
cd /apps/ha
docker-compose pull
docker stop homeassistant
docker remove homeassistant
docker compose up -d
```
