# server-bootstrap

Repositorio genérico para preparar un VPS o servidor Linux base.

Responsabilidad:
- bootstrap inicial del host
- baseline reusable del servidor
- Docker
- Tailscale
- Alloy como servicio host-level
- layout base de `/srv/...`

No contiene:
- Docker Compose de una aplicación concreta
- configuración específica de Alloy para un stack
- deploy de servicios de negocio

## Layout

- `ansible/playbooks/bootstrap.yml`
- `ansible/playbooks/host-baseline.yml`
- `.github/workflows/bootstrap-host.yml`
- `.github/workflows/apply-runtime.yml`
- `tests/ansible/`

## Flujo operativo

1. `bootstrap-host.yml`
   - acceso inicial como `root`
   - usuario admin, hardening, firewall, swap

2. `apply-runtime.yml`
   - acceso como usuario admin
   - Docker, Tailscale, Alloy package y paths base

## Validación local

```bash
make ansible-check
```
