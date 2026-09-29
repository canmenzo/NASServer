**`READ BEFORE INSTALLATING`**
---
// CREATE FOLDERS & VOLUMES AS SPECIFIED BELOW
// REPLACE ALL VOLUMES WITH THE CORRECT VOLUME/PATH NAMES
// REPLACE TZ VALUE WITHIN ENVIRONMENTS WITH YOUR TIMEZONE
// REPLACE ALL PUID/PGIDs BY USING THE INSTRUCTIONS

---


### PLEX INSTALLATION
// Get PLEX_CLAIM from https://plex.tv/claim - it expires 4 minutes after you copy it
docker run -d \
  --name=plex \
  --net=host \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -e VERSION=docker \
  -e PLEX_CLAIM=claim-xxxxxxxxxxxxxxxxxxxx \
  -v /volume1/docker/plex/data:/config \
  -v /volume1/docker/mediaServer/Media:/data \
  --restart unless-stopped \
  lscr.io/linuxserver/plex:latest

### RADARR INSTALLATION
docker run -d \
  --name=radarr \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -p 7878:7878 \
  -v /volume1/docker/radarr/data:/config \
  -v /volume1/docker/mediaServer/Media:/data \
  --restart unless-stopped \
  lscr.io/linuxserver/radarr:latest

### OVERSEER INSTALLATION
docker run -d \
  --name=overseerr \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -p 5055:5055 \
  -v /volume1/docker/overseerr/data:/config \
  --restart unless-stopped \
  lscr.io/linuxserver/overseerr:latest

### PROWLARR INSTALLATION
docker run -d \
  --name=prowlarr \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -p 9696:9696 \
  -v /volume1/docker/prowlarr/data:/config \
  --restart unless-stopped \
  lscr.io/linuxserver/prowlarr:latest


### SONARR INSTALLATION
docker run -d \
  --name=sonarr \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -p 8989:8989 \
  -v /volume1/docker/sonarr/data:/config \
  -v /volume1/docker/mediaServer/Media:/data \
  --restart unless-stopped \
  lscr.io/linuxserver/sonarr:latest


### QBITTORENT INSTALLATION
docker run -d \
  --name=qbittorrent \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -e WEBUI_PORT=8080 \
  -e TORRENTING_PORT=6881 \
  -p 8080:8080 \
  -p 6881:6881 \
  -p 6881:6881/udp \
  -v /volume1/docker/qbittorent/data:/config \
  -v /volume1/docker/mediaServer/Media:/data \
  --restart unless-stopped \
  lscr.io/linuxserver/qbittorrent:latest
