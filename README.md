# Homelab

A small repository for documenting my two-node Proxmox homelab, projects, and lessons learned.

## Hardware

| Hostname | Model | RAM | Storage | Role |
|---|---|---:|---:|---|
| `shinra.home.arpa` | Dell PowerEdge R220 | 32 GB | 4 TB | Primary Proxmox host |
| `avalanche.home.arpa` | HP ProLiant DL320e Gen8 v2 | 24 GB | 2 TB | Secondary Proxmox host |

The `.home.arpa` namespace is used for private home-network DNS.

## Structure

```text
.
├── blog/           # Progress notes and retrospectives
├── docs/           # General homelab documentation
├── infrastructure/ # Reusable configuration and automation
└── projects/       # Notes for individual services and experiments
```

Each directory starts with a short README. Add documentation when it becomes useful rather than trying to define everything up front.

## Current Services

- Proxmox VE
- Samba
- NetBird
- Docker and Docker Compose
- Jellyfin, qBittorrent, Prowlarr, and Seerr
- Experimental Tailscale and AdGuard Home setups

## Security

Do not commit passwords, API keys, authentication tokens, private keys, public IP addresses, or real `.env` files. Use clear placeholders in public examples.

## License

This repository uses the [MIT License](LICENSE).
