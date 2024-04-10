


---
services:
  prowlarr:
    image: lscr.io/linuxserver/prowlarr:latest
    container_name: prowlarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=GMT/UTC
    volumes:
      - /volume1/docker/prowlarr/data:/config
    ports:
      - 9696:9696
    restart: unless-stopped

---
services:
  radarr:
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=GMT/UTC
    volumes:
      - /volume1/docker/radarr/data:/config
      - /volume1/docker/Media/movies:/movies
      - /volume1/docker/Media/downloads:/downloads
    ports:
      - 7878:7878
    restart: unless-stopped

---
services:
  sonarr:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=GMT/UTC
    volumes:
      - /volume1/docker/mediaServer/sonarr/data:/config
      - /volume1/docker/mediaServer/Media/tv:/tv
      - /volume1/docker/mediaServer/Media/downloads:/downloads
    ports:
      - 8989:8989
    restart: unless-stopped

---
services:
  qbittorrent:
    image: lscr.io/linuxserver/qbittorrent:latest
    container_name: qbittorrent
    environment:
      - PUID=1000
      - PGID=1000
      - WEBUI_PORT=8080
      - TZ=GMT/UTC
    volumes:
      - /volume1/docker/mediaServer/qbittorent/data:/config
      - /volume1/docker/mediaServer/Media/downloads:/downloads
    ports:
      - 8080:8080
      - 6881:6881
      - 6881:6881/udp
    restart: unless-stopped

---
services:
  overseerr:
    image: lscr.io/linuxserver/overseerr:latest
    container_name: overseerr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=GMT/UTC
    volumes:
      - /volume1/docker/mediaServer/overseerr/data:/config
    ports:
      - 5055:5055
    restart: unless-stopped