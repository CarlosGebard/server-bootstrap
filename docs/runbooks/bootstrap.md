# Bootstrap Runbook

## Flujo

1. ejecutar `bootstrap-host.yml` con acceso inicial `root` o con `PROD_SSH_USER` si el proveedor exige otro usuario base como `ubuntu`
2. ejecutar `apply-runtime.yml` con usuario admin
3. entregar el host al repo de deploy correspondiente

## Debug OIDC Infisical

Usar `debug-infisical-oidc.yml` cuando falle la carga de secretos desde GitHub Actions hacia Infisical.

La ruta base de lectura en Infisical sale de la GitHub Variable `INFISICAL_SECRET_PATH`. Ejemplo: si defines `/oracle`, el workflow leerá secretos como `PROD_SSH_PRIVATE_KEY` desde esa carpeta base.

Revisar en los logs:

- el paso de validacion debe confirmar que existen `INFISICAL_IDENTITY_ID`, `INFISICAL_PROJECT_SLUG`, `INFISICAL_ENV_SLUG` e `INFISICAL_SECRET_PATH`
- `INFISICAL_SECRET_PATH` debe apuntar a la carpeta correcta dentro del proyecto
- el paso `Infisical/secrets-action` debe completar y el assert final debe encontrar `PROD_HOST` y `PROD_SSH_PRIVATE_KEY`

## Contrato entregado

El host queda con:
- usuario admin operativo
- Docker y Docker Compose plugin
- Tailscale instalado
- Alloy instalado y habilitado
- layout base de `/srv/...`
