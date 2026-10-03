# 🏠 Homelab Infrastructure Documentation
**Last Updated:** 2026-10-03
**Environment:** Proxmox VE Cluster (`pve1`, `pve2`, `pve3`)

---

## 🖥️ Hardware Inventory
| Node | Model | CPU | RAM | Primary Storage | Role | Operating System | IP Address |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **pve1** | MINISFORUM M1-1295 | i9-12950HX (16C/24T) | 32GB | 1TB NVMe | Primary Compute | Proxmox VE 9.2 | `192.168.3.1` |
| **pve2** | MINISFORUM M1-1295 | i9-12950HX (16C/24T) | 32GB | 1TB NVMe | Secondary Compute | Proxmox VE 9.2 | `192.168.3.2` | 
| **pve3** | Beelink EQ12 | Intel N100 (4C/4T) | 16GB | 500GB SSD | Quorum / HA DNS | Proxmox VE 9.2 | `192.168.3.3` |

---

## 📦 Proxmox Virtual Resources (VMs & LXCs)

### Node: pve1
| VMID | Name | IP Address | Service Type | Operating System | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| CT100 | `lxc-pihole-1` | `192.168.3.100` | Ad-blocking/DNS | Debian 13 | Running |
| CT101 | `lxc-docker-1` | `192.168.3.101` | Management Stack | Debian 13 | Running |
| CT102 | `lxc-arrstack-1` | `192.168.3.102` | Media Stack | Debian 13 | Running |

### Node: pve2
| VMID | Name | IP Address | Service Type | Operating System | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| CT200 | `lxc-pihole-2` | `192.168.3.200` | Ad-blocking/DNS | Debian 13 | Running |
| CT201 | `lxc-docker-2` | `192.168.3.201` | Ingress/Web | Debian 13 | Running |

### Node: pve3
| VMID | Name | IP Address | Service Type | Operating System | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| VM253 | `vm-pbs` | `192.168.3.253` | Proxmox Backup Server | PBS OS (Debian 13) | Running |
| CT254 | `lxc-pihole-3` | `192.168.3.254` | Ad-blocking/DNS | Debian 13 | Running |

---

## 🔌 Service Port Mappings
| Service | Parent Host | Internal IP | Port | Access Type |
| :--- | :--- | :--- | :--- | :--- |
| **Pi-hole Admin** | `pihole-[1-3]` | `.100 / .200 / .254` | `80` | HTTP |
| **PBS Admin UI** | `vm-pbs` | `192.168.3.253` | `8007` | HTTPS |
| **NPM Admin** | `lxc-docker-2` | `192.168.3.201` | `81` | HTTP |
| **Portainer** | `docker-[1-2]` | `.101 / .201` | `9443` | HTTPS |
| **Uptime Kuma** | `lxc-docker-1` | `192.168.3.101` | `3001` | HTTP |
| **Overseerr** | `lxc-arrstack-1` | `192.168.3.102` | `5055` | HTTP |
| **Radarr** | `lxc-arrstack-1` | `192.168.3.102` | `7878` | HTTP |
| **Sonarr** | `lxc-arrstack-1` | `192.168.3.102` | `8989` | HTTP |
| **Prowlarr** | `lxc-arrstack-1` | `192.168.3.102` | `9696` | HTTP |
| **qBittorrent** | `lxc-arrstack-1` | `192.168.3.102` | `8080` | HTTP |
| **NZBGet** | `lxc-arrstack-1` | `192.168.3.102` | `6789` | HTTP |

---

## 🐋 Docker Service Topology

### 🛠️ Infrastructure Management (`lxc-docker-1` - `.101`)
* **nebula-sync:** Core synchronization of Pi-hole blocklists and DNS records.
* **uptime-kuma:** Service monitoring and uptime dashboard.
* **cloudflare:** Secure tunnel for remote access.
* **watchtower:** Automated container image updates.
* **portainer:** Web UI for Docker management.

### 🌐 Web Ingress & Proxy (`lxc-docker-2` - `.201`)
* **nginx-proxy-manager:** Reverse proxy handling SSL/TLS and routing.
* **npm-db:** MariaDB backend for proxy configurations.
* **goaccess:** Real-time traffic analytics.

### 🎬 Media Automation Stack (`lxc-arrstack-1` - `.102`)
* **Requests:** `overseerr`, `doplarr` (Discord Bot).
* **Management:** `sonarr`, `radarr`, `prowlarr`.
* **Downloaders:** `qbittorrent`, `nzbget`.
