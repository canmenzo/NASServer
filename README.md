### NASServer

- This is my NAS Server project.
  - In this repo, I'll document the installation instructions for CLI as well as docker compose for the following softwARRs:
    - `Prowlarr`, `Radarr`, `Sonarr`, `qBittorrent`, `Overseerr`, `Plex`,

### Instructions

- There are key points that one must understand before using the docker.md files that are within this repo to install:
    - > `PUID` & `PGID`s are user and group IDs for unix.
    - When installing docker containers, create a new user account that is not root.
      - After account creation, use `id $user` to obtain both values.
      - Replace the values within the docker compose, and you are set.
      - *Using root accounts for docker containers that are going to be externally public will expose security risks, and possible vulnerabilities if not used correctly.*
      - > _Reference_ - [PUID & PGID](https://docs.linuxserver.io/general/understanding-puid-and-pgid/#why-use-these)


- [Plex](https://hub.docker.com/r/linuxserver/plex)
    generate 2 api key for radarr and sonarr
- [Radarr](https://hub.docker.com/r/linuxserver/radarr)
    settings - connect - add plex's api
    settings - download clients - qbittorent's username and password
- [Sonarr](https://hub.docker.com/r/linuxserver/sonarr)
    settings - connect - add plex's api
    settings - download clients - qbittorent's username and password
- [Prowlarr](https://hub.docker.com/r/linuxserver/prowlarr)
    settings - apps - add radarr's api
    settings - apps - add sonarr's api
- [qbittorent](https://hub.docker.com/r/linuxserver/qbittorrent)
    check logs for admin password | username is `admin`
- [Overseerr](https://hub.docker.com/r/linuxserver/qbittorrent)
    go to radar and sonarr (settings-general), generate api
    when you set-up plex add radar and sonar settings with the said api 