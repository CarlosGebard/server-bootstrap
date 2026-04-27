## Goal

Permitir que el workflow de bootstrap use un usuario SSH inicial configurable, para soportar proveedores como Oracle Cloud que exigen `ubuntu` en lugar de `root`.

## Scope

- hacer configurable el usuario SSH de `bootstrap-host.yml`
- conservar `root` como valor por defecto para no romper flujos existentes
- documentar la nueva variable operativa en el runbook y el inventario de secretos

## Assumptions

- el usuario inicial alternativo tiene permisos `sudo` sin fricción para que `become: true` siga funcionando
- `apply-runtime.yml` no necesita este ajuste porque ya entra con el usuario admin post-bootstrap
- el secreto/variable seguirá llegando desde Infisical como `PROD_SSH_*`

## Steps

1. Ajustar `.github/workflows/bootstrap-host.yml` para leer `PROD_SSH_USER` y usar `root` por defecto.
2. Documentar `PROD_SSH_USER` en `docs/secrets-and-variables.md` y `docs/runbooks/bootstrap.md`.
3. Revisar diff y validaciones locales disponibles.

## Validation

- inspeccionar diff final
- ejecutar `git diff --check`
- ejecutar checks locales adicionales si no requieren dependencias ausentes

## Risks

- asumir `sudo` disponible para el usuario inicial puede fallar en imágenes endurecidas
- si `PROD_SSH_USER` se configura mal, el error cambia de forma pero sigue bloqueando el acceso SSH
