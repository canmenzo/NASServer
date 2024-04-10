
### RADARR INSTALLATION
docker run -d \
  --name=radarr \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=GMT/UTC \
  -p 7878:7878 \
  -v /volume1/docker/radarr/data:/config \
  -v /volume1/docker/mediaServer/Media/movies:/movies \
  -v /volume1/docker/mediaServer/Media/downloads:/downloads \
  --restart unless-stopped \
  lscr.io/linuxserver/radarr:latest

### OVERSEER INSTALLATION
docker run -d \
  --name=overseerr \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=GMT/UTC \
  -p 5055:5055 \
  -v /volume1/docker/overseerr/data:/config \
  --restart unless-stopped \
  lscr.io/linuxserver/overseerr:latest

### PROWLARR INSTALLATION
docker run -d \
  --name=prowlarr \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=GMT/UTC \
  -p 9696:9696 \
  -v /volume1/docker/prowlarr/data:/config \
  --restart unless-stopped \
  lscr.io/linuxserver/prowlarr:latest


### SONARR INSTALLATION
docker run -d \
  --name=sonarr \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=GMT/UTC \
  -p 8989:8989 \
  -v /volume1/docker/sonarr/data:/config \
  -v /volume1/docker/mediaServer/Media/tv:/tv \
  -v /volume1/docker/mediaServer/Media/downloads:/downloads \
  --restart unless-stopped \
  lscr.io/linuxserver/sonarr:latest


### QBITTORENT INSTALLATION
docker run -d \
  --name=qbittorrent \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=GMT/UTC \
  -e WEBUI_PORT=8080 \
  -e TORRENTING_PORT=6881 \
  -p 8080:8080 \
  -p 6881:6881 \
  -p 6881:6881/udp \
  -v /volume1/docker/qbittorent/data:/config \
  -v /volume1/docker/mediaServer/Media/downloads:/downloads \
  --restart unless-stopped \
  lscr.io/linuxserver/qbittorrent:latest