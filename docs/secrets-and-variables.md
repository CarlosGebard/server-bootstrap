# Secrets y Variables

## GitHub Variables

- `INFISICAL_IDENTITY_ID`
- `INFISICAL_PROJECT_SLUG`
- `INFISICAL_ENV_SLUG`
- `INFISICAL_SECRET_PATH` ruta base dentro de Infisical, por ejemplo `/oracle`

## GitHub Workflow Inputs

- `git_ref` para workflows operativos

## Infisical

- `PROD_HOST`
- `PROD_SSH_PRIVATE_KEY`
- `PROD_SSH_PORT` opcional
- `PROD_SSH_USER` opcional para bootstrap inicial, por defecto `root`
- `PROD_SSH_KNOWN_HOSTS` opcional
- `TAILSCALE_AUTH_KEY`
- `SERVER_HOST` IP o hostname Tailscale del servidor para `provision-tailscale-host.yml`
- `TAILSCALE_SERVER_HOST` IP o hostname Tailscale del servidor para `provision-tailscale-host.yml`
- `TAILSCALE_HOSTNAME` opcional

## Provision por Tailscale

`provision-tailscale-host.yml` conecta el runner de GitHub Actions a Tailscale antes de ejecutar Ansible.

Secretos requeridos:

- `TAILSCALE_AUTH_KEY`
- `SERVER_HOST` o `TAILSCALE_SERVER_HOST`
- `PROD_SSH_PRIVATE_KEY`

Secretos opcionales:

- `PROD_SSH_PORT`, por defecto `22`
- `PROD_SSH_USER`, por defecto `root` solo para bootstrap
- `PROD_SSH_KNOWN_HOSTS`; si no existe, el workflow ejecuta `ssh-keyscan` sobre el host Tailscale configurado
