# 📁 NASServer

---

This is my NAS Server project.

In this repo, I'll document the installation instructions for CLI as well as Docker Compose for the following softwARRs:

- `Prowlarr`
- `Radarr`
- `Sonarr`
- `qBittorrent`
- `Overseerr`
- `Plex`

Plus one tool of my own, in its own repo:

- [**Watchlistrr**](https://github.com/canmenzo/watchlistrr) — Seerr can only sync a *Plex*
  watchlist, so this fills the gap: it reads my public Letterboxd watchlist every 15 minutes,
  resolves each new film to its TMDB id, and requests it in Seerr, which hands it to Radarr.

---

## ⚙️ Instructions

Before using the `docker.md` files in this repo, there are a few key things to understand:

- `PUID` & `PGID` are user and group IDs for Unix systems.
- Do **not** use the root account for Docker containers that are externally accessible.

### ✅ To Do:
1. Create a **new user** account (not root).
2. Run `id $user` to obtain the `PUID` and `PGID`.
3. Replace these values in the Docker Compose files.

> 🔐 *Using root for public-facing containers exposes you to unnecessary security risks.*

📚 **Reference**: [PUID & PGID Guide](https://docs.linuxserver.io/general/understanding-puid-and-pgid/#why-use-these)

---

## 📦 Container Notes

### [Plex](https://hub.docker.com/r/linuxserver/plex)
- Generate **two API keys** for Radarr and Sonarr.

### [Radarr](https://hub.docker.com/r/linuxserver/radarr)
- `Settings > Connect`: Add Plex's API  
- `Settings > Download Clients`: Add qBittorrent's username and password

### [Sonarr](https://hub.docker.com/r/linuxserver/sonarr)
- `Settings > Connect`: Add Plex's API  
- `Settings > Download Clients`: Add qBittorrent's username and password

### [Prowlarr](https://hub.docker.com/r/linuxserver/prowlarr)
- `Settings > Apps`: Add Radarr’s and Sonarr’s API keys

### [qBittorrent](https://hub.docker.com/r/linuxserver/qbittorrent)
- Default credentials:
  - Username: `admin`
  - Password: *(check container logs)*

### [Overseerr](https://hub.docker.com/r/linuxserver/qbittorrent)
- In **Radarr** and **Sonarr**:  
  - `Settings > General`: Generate API key  
- During Plex setup, input the Radarr and Sonarr API keys

---
