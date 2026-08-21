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

- [`letterboxd-overseerr-sync`](https://github.com/canmenzo/letterboxd-overseerr-sync) — puts my Letterboxd watchlist into Overseerr

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

## 🎬 Bonus: Letterboxd → Overseerr

Overseerr/Seerr can't read a Letterboxd watchlist — its only watchlist source is Plex. If
you keep your to-watch list on Letterboxd like I do, that means adding every film twice.

So I wrote a tool that closes the gap, and put it in its own repo:

### 👉 [canmenzo/letterboxd-overseerr-sync](https://github.com/canmenzo/letterboxd-overseerr-sync)

It reads your (public) Letterboxd watchlist, resolves each film to its **TMDB id** — matching
by id rather than by title, so you never get the wrong *Nosferatu* — and then either:

- **requests it straight into Overseerr** through the API (recommended), or
- **adds it to your Plex watchlist**, which Overseerr's own watchlist sync picks up on its
  ~15–20 minute cycle.

Runs as a Docker container next to the rest of this stack, or from cron. MIT licensed —
help yourself.

```bash
git clone https://github.com/canmenzo/letterboxd-overseerr-sync.git
cd letterboxd-overseerr-sync
cp .env.example .env      # LETTERBOXD_USERNAME, OVERSEERR_URL, OVERSEERR_API_KEY
docker compose run --rm letterboxd-sync --check
docker compose up -d
```

Setup, the full configuration reference and a comparison against the other community
options are all in [that repo's README](https://github.com/canmenzo/letterboxd-overseerr-sync#readme).

---
