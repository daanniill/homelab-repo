# Media Stack

Docker Compose deployment for Jellyfin, qBittorrent, Prowlarr, and Seerr. See [`compose.yaml`](compose.yaml).

## Setup

Create an untracked `.env` file and adjust the paths and bind address:

```env
BIND_ADDRESS=<SERVER-IP>
CONFIG_ROOT=/path/to/appdata
CACHE_ROOT=/path/to/cache
MEDIA_ROOT=/path/to/media
DOWNLOAD_ROOT=/path/to/downloads
PUID=1000
PGID=1000
TZ=America/Los_Angeles
```

The Seerr configuration directory must be writable by UID/GID `1000:1000`.

Deploy the stack:

```bash
docker compose config && docker compose pull && docker compose up -d
```

## Web Interfaces

| Service | URL |
|---|---|
| Jellyfin | `http://<SERVER-IP>:8096` |
| qBittorrent | `http://<SERVER-IP>:8080` |
| Prowlarr | `http://<SERVER-IP>:9696` |
| Seerr | `http://<SERVER-IP>:5055` |

Containers on the Compose network can use service names such as `http://jellyfin:8096` and `http://qbittorrent:8080`.

## Management

```bash
docker compose ps
docker compose logs -f
docker compose down
```
