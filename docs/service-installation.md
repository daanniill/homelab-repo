## Service Installation Commands

> These commands are intended for Debian or Ubuntu VMs/LXC containers. Do not run them directly on the Proxmox host unless the service is specifically meant to run there.

### AdGuard Home

Provides network-wide DNS filtering and domain blocking.

```bash
sudo apt update && sudo apt install -y curl && curl -sSL https://raw.githubusercontent.com/AdguardTeam/AdGuardHome/master/scripts/install.sh | sh -s -- -v
```

Default setup interface:

```text
http://<SERVER-IP>:3000
```

---

### Samba

Provides SMB file sharing for Windows, macOS, and Linux clients.

```bash
sudo apt update && sudo apt install -y samba smbclient
```

The main configuration file is:

```text
/etc/samba/smb.conf
```

After editing the configuration:

```bash
sudo testparm && sudo systemctl restart smbd
```

---

### NetBird

Provides secure remote access to the homelab through a WireGuard-based private network.

```bash
curl -fsSL https://pkgs.netbird.io/install.sh | sh && sudo netbird up
```

Check the connection:

```bash
netbird status
```

For unattended server setup, use a setup key without committing the real key to GitHub:

```bash
sudo netbird up --setup-key <NETBIRD_SETUP_KEY>
```

---

### Tailscale

Previously used for secure remote access and VPN experimentation.

```bash
curl -fsSL https://tailscale.com/install.sh | sh && sudo tailscale up
```

Check the connection:

```bash
tailscale status
```

---

### Jellyfin

Provides media library management and streaming.

```bash
curl -sSLO https://repo.jellyfin.org/install-debuntu.sh && curl -sSLO https://repo.jellyfin.org/install-debuntu.sh.sha256sum && sha256sum -c install-debuntu.sh.sha256sum && sudo bash install-debuntu.sh
```

Default web interface:

```text
http://<SERVER-IP>:8096
```

---

### qBittorrent

Provides a headless BitTorrent client with a web interface.

```bash
sudo apt update && sudo apt install -y qbittorrent-nox
```

Run it for the first time:

```bash
qbittorrent-nox
```

Default web interface:

```text
http://<SERVER-IP>:8080
```

For a permanent installation, run qBittorrent through a dedicated systemd service account rather than leaving it attached to a terminal.

---

### Docker

Provides the container runtime for the media stack.

```bash
curl -fsSL https://get.docker.com | sudo sh
```

Enable Docker at startup:

```bash
sudo systemctl enable --now docker
```

Verify the installation:

```bash
sudo docker run --rm hello-world
```

> Docker describes `get.docker.com` as a convenience installer. For a production-oriented rebuild, use Docker's official Debian repository installation procedure.

---

### Media Stack

When the repository contains a completed `compose.yml` file for Jellyfin, qBittorrent, Prowlarr, and Seerr:

```bash
docker compose pull && docker compose up -d
```

Start only the listed media services:

```bash
docker compose up -d jellyfin qbittorrent prowlarr seerr
```

Stop the stack:

```bash
docker compose down
```

View its status:

```bash
docker compose ps
```

Follow service logs:

```bash
docker compose logs -f
```

---

### Prowlarr

Prowlarr manages indexers used by the media automation services.

When Prowlarr is defined in the media stack's `compose.yml`:

```bash
docker compose up -d prowlarr
```

Default web interface:

```text
http://<SERVER-IP>:9696
```

---

### Seerr

Seerr provides a request-management interface connected to Jellyfin.

When Seerr is defined in the media stack's `compose.yml`:

```bash
docker compose up -d seerr
```

Default web interface:

```text
http://<SERVER-IP>:5055
```

---

## Rebuild the Entire Docker Stack

From the directory containing `compose.yml`:

```bash
docker compose pull && docker compose up -d
```

This downloads newer container images if available and recreates the services while preserving data stored in properly configured bind mounts or named volumes.


