# Secrets y Variables

## GitHub Variables

- `INFISICAL_IDENTITY_ID`
- `INFISICAL_PROJECT_SLUG`
- `INFISICAL_ENV_SLUG`
- `INFISICAL_SECRET_PATH` ruta base dentro de Infisical, por ejemplo `/oracle`

## GitHub Workflow Inputs

- `git_ref` para los workflows de bootstrap

## Infisical

- `PROD_HOST`
- `PROD_SSH_PRIVATE_KEY`
- `PROD_SSH_PORT` opcional
- `PROD_SSH_USER` opcional para bootstrap inicial, por defecto `root`
- `PROD_SSH_KNOWN_HOSTS` opcional
- `TAILSCALE_AUTH_KEY`
- `TAILSCALE_HOSTNAME` opcional
- `ADMIN_SSH_AUTHORIZED_KEY` clave pública SSH del usuario admin para el primer
  bootstrap local en la Raspberry Pi

## Bootstrap local en Raspberry Pi

`bootstrap-raspberry-pi.yml` usa un runner instalado en la propia Raspberry Pi.
No requiere `PROD_HOST` ni credenciales SSH para acceder al host. El runner debe
tener las etiquetas `self-hosted`, `linux` y `raspberry-pi`, y ejecutarse con un
usuario que pueda usar `sudo` sin contraseña.

Secretos requeridos en la ruta de Infisical:

- `ADMIN_SSH_AUTHORIZED_KEY`
- `TAILSCALE_AUTH_KEY`

El workflow usa OIDC con las mismas variables `INFISICAL_*` del entorno
`production` y ejecuta ambos playbooks contra `localhost`.
