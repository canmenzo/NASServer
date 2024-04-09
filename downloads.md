 
services:
  jellyfin:
    image: docker.io/linuxserver/jellyfin
    container_name: jellyfin
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Turkey
    volumes:
      - /home/media/docker/jellyfin.config:/config
      - /home/media/Media/tv:/data/tvshows
      - /home/media/Media/movies:/data/movies
    ports:
      - 8096:8096/tcp
      - 7359:7359/udp
    restart: unless-stopped

---
services:
  prowlarr:
    image: lscr.io/linuxserver/prowlarr:latest
    container_name: prowlarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Turkey
    volumes:
      - /home/media/docker/prowlarr/config:/config
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
      - TZ=Turkey
    volumes:
      - /home/media/docker/radarr/config:/config
      - /home/media/Media/movies:/movies
      - /home/media/Media/downloads:/downloads
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
      - TZ=Turkey
    volumes:
      - /home/media/docker/sonarr/config:/config
      - /home/media/Media/tv:/tv
      - /home/media/Media/downloads:/downloads
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
      - TZ=Turkey
      - WEBUI_PORT=8080
    volumes:
      - /home/media/docker/qbittorent/config:/config
      - /home/media/Media/downloads:/downloads
    ports:
      - 8080:8080
      - 6881:6881
      - 6881:6881/udp
    restart: unless-stopped

---
version: '3'
services:
    jellyseerr:
       image: fallenbagel/jellyseerr:latest
       container_name: jellyseerr
       environment:
            - LOG_LEVEL=debug
            - TZ=Turkey
       ports:
            - 5055:5055
       volumes:
            - /home/media/docker/jellyseerr/config:/app/config
       restart: unless-stopped 