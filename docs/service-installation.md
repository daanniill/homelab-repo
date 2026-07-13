# Service Installation Commands

Quick-reference commands for the services used in this homelab.

> Run these only inside the intended Debian or Ubuntu VM/LXC container. Do not run application installers directly on a Proxmox host. Review remote scripts before running them, and never place real credentials or setup keys in this file.

## Base Services

### Samba

```bash
sudo apt update && sudo apt install -y samba smbclient && sudo systemctl enable --now smbd
```

### Docker Engine and Docker Compose

Docker's convenience installer is intended for development and homelab use. Review the script before running it.

```bash
curl -fsSL https://get.docker.com | sudo sh && sudo systemctl enable --now docker && docker compose version
```

## Remote Access

### NetBird

```bash
curl -fsSL https://pkgs.netbird.io/install.sh | sh && sudo netbird up
```

For unattended enrollment, provide the setup key through a protected secret-management process rather than committing it here.

### Tailscale

Tailscale remains experimental in this homelab.

```bash
curl -fsSL https://tailscale.com/install.sh | sh && sudo tailscale up
```

## DNS

### AdGuard Home

AdGuard Home remains experimental in this homelab.

```bash
curl -sSL https://raw.githubusercontent.com/AdguardTeam/AdGuardHome/master/scripts/install.sh | sudo sh -s -- -v
```

After installation, complete the initial configuration at `http://<SERVER-IP>:3000`.

## Media Stack

These commands assume the current directory contains a `compose.yaml` file with services named `jellyfin`, `qbittorrent`, `prowlarr`, and `seerr`.

### Deploy the Entire Stack

```bash
docker compose pull && docker compose up -d
```

### Jellyfin

```bash
docker compose pull jellyfin && docker compose up -d jellyfin
```

### qBittorrent

```bash
docker compose pull qbittorrent && docker compose up -d qbittorrent
```

### Prowlarr

```bash
docker compose pull prowlarr && docker compose up -d prowlarr
```

### Seerr

```bash
docker compose pull seerr && docker compose up -d seerr
```

## Common Operations

```bash
docker compose ps
```

```bash
docker compose logs -f
```

```bash
docker compose down
```

## Proxmox VE

Proxmox VE is installed from its installer ISO and is not represented by a one-line application install command. General services should run in VMs or LXC containers rather than directly on the Proxmox hosts.

## Official References

- [Docker Engine installation](https://docs.docker.com/engine/install/)
- [NetBird Linux installation](https://docs.netbird.io/get-started/install/linux)
- [Tailscale Linux installation](https://tailscale.com/docs/install/linux)
- [AdGuard Home installation](https://github.com/AdguardTeam/AdGuardHome#getting-started)
