## Goal

Simplificar el workflow manual de debug OIDC de Infisical para que use el action oficial con la menor cantidad posible de pasos y configuracion fija.

## Scope

- reemplazar el workflow de debug detallado por uno minimo
- seguir usando GitHub Variables para la configuracion de Infisical
- ajustar la documentacion del repo al nuevo flujo

## Assumptions

- `INFISICAL_IDENTITY_ID`, `INFISICAL_PROJECT_SLUG`, `INFISICAL_ENV_SLUG` y `INFISICAL_SECRET_PATH` existen como GitHub Variables
- el objetivo del workflow es confirmar que el fetch por OIDC funciona, no inspeccionar claims JWT
- validar `PROD_HOST` y `PROD_SSH_PRIVATE_KEY` sigue siendo suficiente para este repo

## Steps

1. Reemplazar `.github/workflows/debug-infisical-oidc.yml` por una version minima basada en `Infisical/secrets-action`.
2. Mantener una validacion previa de variables requeridas.
3. Ejecutar el fetch OIDC y dejar un check final de secretos esperados.
4. Actualizar `docs/secrets-and-variables.md`, `.github/workflows/README.md` y `docs/runbooks/bootstrap.md`.

## Validation

- revisar sintaxis YAML del workflow
- revisar consistencia entre workflow y documentacion
- inspeccionar diff final

## Risks

- perder capacidad de diagnostico fino sobre audience o claims del JWT
- asumir que un fallo del action oficial alcanza como senal suficiente para troubleshooting inicial
