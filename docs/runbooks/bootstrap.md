# Bootstrap Runbook

## Flujo

1. ejecutar `bootstrap-host.yml` con acceso inicial `root`
2. ejecutar `apply-runtime.yml` con usuario admin
3. entregar el host al repo de deploy correspondiente

## Debug OIDC Infisical

Usar `debug-infisical-oidc.yml` cuando falle la carga de secretos desde GitHub Actions hacia Infisical.

La ruta base de lectura en Infisical sale de la GitHub Variable `INFISICAL_SECRET_PATH`. Ejemplo: si defines `/oracle`, el workflow leerá secretos como `PROD_SSH_PRIVATE_KEY` desde esa carpeta base.

Revisar en los logs:

- `iss` debe apuntar a `https://token.actions.githubusercontent.com`
- `sub` debe coincidir con el patron configurado en la machine identity de Infisical
- `aud` debe coincidir con la audiencia esperada por la machine identity
- `INFISICAL_SECRET_PATH` debe apuntar a la carpeta correcta dentro del proyecto
- el paso de login OIDC contra Infisical debe responder `success: true`
- el paso `Infisical/secrets-action` debe completar y el assert final debe encontrar `PROD_HOST` y `PROD_SSH_PRIVATE_KEY`

Si usas Infisical self-hosted, ejecutar el workflow con `infisical_domain` apuntando a tu dominio base.

## Contrato entregado

El host queda con:
- usuario admin operativo
- Docker y Docker Compose plugin
- Tailscale instalado
- Alloy instalado y habilitado
- layout base de `/srv/...`
