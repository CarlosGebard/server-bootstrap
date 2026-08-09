# ADR 0001: Bootstrap local de Raspberry Pi con GitHub Actions

## Contexto

La Raspberry Pi es el host objetivo y no dispone de IP pública para que un
runner hospedado por GitHub acceda mediante SSH. El bootstrap debe continuar
obteniendo sus secretos desde Infisical.

## Decisión

Se ejecutará `bootstrap-raspberry-pi.yml` en un runner de GitHub Actions
instalado en la propia Raspberry Pi. El workflow usa OIDC para obtener secretos
de Infisical y ejecuta ambos playbooks Ansible con conexión local.

Durante el primer bootstrap, `ADMIN_SSH_AUTHORIZED_KEY` permite crear la clave
autorizada del usuario administrador cuando no existe una clave en root.

## Consecuencias

El runner debe estar registrado antes de ejecutar el workflow, llevar las
etiquetas requeridas y usar un usuario con `sudo` sin contraseña. No se necesita
IP pública ni SSH remoto para aplicar el bootstrap.
