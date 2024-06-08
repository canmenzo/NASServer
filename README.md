### NASServer

- This is my NAS Server project.
  - In this repo, I'll document the installation instructions for CLI as well as docker compose for the following softwARRs:
    - `Prowlarr`, `Radarr`, `Sonarr`, `qBittorrent`, `Overseerr`, `Plex`,

### Instructions
- Plex
    generate 2 api key for radarr and sonarr
- radarr
    settings - connect - add plex's api
    settings - download clients - qbittorent's username and password
- sonarr
    settings - connect - add plex's api
    settings - download clients - qbittorent's username and password
- prowlarr
    settings - apps - add radarr's api
    settings - apps - add sonarr's api
- qbittorent
    check logs for admin password | username is `admin`
- overseerr
    go to radar and sonarr (settings-general), generate api
    when you set-up plex add radar and sonar settings with the said api 