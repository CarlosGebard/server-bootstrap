# Secrets y Variables

## GitHub Variables

- `INFISICAL_IDENTITY_ID`
- `INFISICAL_PROJECT_SLUG`
- `INFISICAL_ENV_SLUG`
- `INFISICAL_SECRET_PATH` ruta base dentro de Infisical, por ejemplo `/oracle`

## GitHub Workflow Inputs

- `git_ref` para workflows operativos
- `oidc_audience` opcional para el workflow `debug-infisical-oidc.yml`
- `infisical_domain` opcional para el workflow `debug-infisical-oidc.yml`

## Infisical

- `PROD_HOST`
- `PROD_SSH_PRIVATE_KEY`
- `PROD_SSH_PORT` opcional
- `PROD_SSH_KNOWN_HOSTS` opcional
- `TAILSCALE_AUTH_KEY`
- `TAILSCALE_HOSTNAME` opcional
