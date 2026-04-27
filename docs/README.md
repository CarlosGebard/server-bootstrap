# Docs Overview

`server-bootstrap` prepara capacidades reutilizables del host.

## Capas

- `bootstrap`
  - usuario admin
  - SSH hardening
  - fail2ban / ufw
  - swap

- `host-baseline`
  - Docker
  - Tailscale
  - Alloy package y servicio
  - paths base `/srv`, `/srv/apps`, `/srv/data`, `/srv/logs`, `/srv/secrets`, `/srv/backups`
