# Bootstrap Runbook

## Flujo

1. ejecutar `bootstrap-host.yml` con acceso inicial `root` o con `PROD_SSH_USER` si el proveedor exige otro usuario base como `ubuntu`
2. el workflow aplica bootstrap y baseline completo en la misma ejecución
3. entregar el host al repo de deploy correspondiente

## Bootstrap local en Raspberry Pi

Para bootstrapear una Raspberry Pi que no tiene IP pública, instalar primero un
runner de GitHub Actions en ella con las etiquetas `self-hosted`, `linux` y
`raspberry-pi`. El usuario que ejecuta el runner debe tener `sudo` sin
contraseña.

En Infisical, configurar `ADMIN_SSH_AUTHORIZED_KEY` con la clave pública que se
instalará para el usuario admin y `TAILSCALE_AUTH_KEY` para la primera unión a
la tailnet. Luego ejecutar `bootstrap-raspberry-pi.yml` desde GitHub Actions.

El workflow obtiene los secretos por OIDC y ejecuta bootstrap y runtime contra
`localhost`; no usa `PROD_HOST`, IP pública ni SSH remoto.

En Debian 13 el workflow usa el Python nativo dentro de un entorno virtual e
instala `python3-venv` automáticamente. El runner necesita salida a APT y PyPI
durante el bootstrap.

## Debug OIDC Infisical

Usar `debug-infisical-oidc.yml` cuando falle la carga de secretos desde GitHub Actions hacia Infisical.

La ruta base de lectura en Infisical sale de la GitHub Variable `INFISICAL_SECRET_PATH`. Ejemplo: si defines `/oracle`, el workflow leerá secretos como `PROD_SSH_PRIVATE_KEY` desde esa carpeta base.

Revisar en los logs:

- el paso de validacion debe confirmar que existen `INFISICAL_IDENTITY_ID`, `INFISICAL_PROJECT_SLUG`, `INFISICAL_ENV_SLUG` e `INFISICAL_SECRET_PATH`
- `INFISICAL_SECRET_PATH` debe apuntar a la carpeta correcta dentro del proyecto
- el paso `Infisical/secrets-action` debe completar y el assert final debe encontrar `ADMIN_SSH_AUTHORIZED_KEY`, `PROD_HOST`, `PROD_SSH_PRIVATE_KEY` y `TAILSCALE_AUTH_KEY`

## Contrato entregado

El host queda con:
- usuario admin operativo
- Docker y Docker Compose plugin
- Tailscale instalado
- Alloy instalado y habilitado
- layout base de `/srv/...`
