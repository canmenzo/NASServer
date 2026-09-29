# 📁 NASServer

[![license](https://img.shields.io/github/license/canmenzo/NASServer)](LICENSE)
![docker](https://img.shields.io/badge/docker-compose-2496ED?logo=docker&logoColor=white)
![platform](https://img.shields.io/badge/platform-Synology%20DSM-B5B5B6?logo=synology&logoColor=white)

Notes and Docker configs for my home NAS media stack: Plex, Radarr, Sonarr, Prowlarr, qBittorrent and Overseerr, all on linuxserver.io images. Written for a Synology box (`/volume1/...` paths), but it works on any Docker host once the paths are changed.

### ✨ Features
- 🐳 [`docker-compose.yml`](docker-compose.yml): the live stack (qBittorrent, Sonarr, Radarr)
- 📋 [`dockerCompose.md`](dockerCompose.md): one compose snippet per service, including Prowlarr and Overseerr
- 💻 [`dockerCLI.md`](dockerCLI.md): the same services as plain `docker run` commands, plus Plex
- 🔗 Every service that touches media mounts one `Media` folder as `/data`, so downloads, `tv` and `movies` share a filesystem and imports can hardlink instead of copy
- 🎬 Companion tool: [Watchlistrr](https://github.com/canmenzo/watchlistrr) syncs a Letterboxd watchlist into Seerr/Overseerr by TMDB id, which then hands it to Radarr

### 🚀 Quick start

1. Create a non-root user to own the media folders and run `id <user>` to get its `PUID` and `PGID`.
2. Create the folders:
   ```
   Media/downloads   -> /data/downloads   (qBittorrent save path)
   Media/tv          -> /data/tv          (Sonarr root folder)
   Media/movies      -> /data/movies      (Radarr root folder)
   ```
3. Edit `docker-compose.yml`: set `PUID`/`PGID`, `TZ`, and the host paths, then:
   ```bash
   docker compose up -d
   ```
4. Add the other services from `dockerCompose.md` or `dockerCLI.md` the same way.

> 🔐 Do not run externally reachable containers as root. See the [PUID & PGID guide](https://docs.linuxserver.io/general/understanding-puid-and-pgid/#why-use-these).

### ⚙️ Configuration

| Service | Port | Wiring |
|---|---|---|
| [Plex](https://hub.docker.com/r/linuxserver/plex) | 32400 (host network) | Get `PLEX_CLAIM` from [plex.tv/claim](https://plex.tv/claim) (expires in 4 minutes). Generate API keys for Radarr and Sonarr. |
| [Radarr](https://hub.docker.com/r/linuxserver/radarr) | 7878 | `Settings > Connect`: add Plex. `Settings > Download Clients`: add qBittorrent's username and password. |
| [Sonarr](https://hub.docker.com/r/linuxserver/sonarr) | 8989 | Same as Radarr. |
| [Prowlarr](https://hub.docker.com/r/linuxserver/prowlarr) | 9696 | `Settings > Apps`: add Radarr's and Sonarr's API keys. |
| [qBittorrent](https://hub.docker.com/r/linuxserver/qbittorrent) | 8080 (web), 6881 (torrent) | Username `admin`; the temporary password is in the container logs. |
| [Overseerr](https://hub.docker.com/r/linuxserver/overseerr) | 5055 | Generate API keys in Radarr and Sonarr (`Settings > General`) and enter them during setup. |

No secrets live in this repo: API keys are generated in each app's own UI.

### 📄 License

MIT
