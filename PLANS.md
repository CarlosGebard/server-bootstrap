## Goal

Agregar un workflow manual para diagnosticar la autenticacion OIDC entre GitHub Actions e Infisical sin exponer JWTs ni secretos en logs.

## Scope

- crear un workflow de debug OIDC para Infisical
- parametrizar la ruta base de secretos en los workflows operativos y de debug
- documentar el uso y los puntos de validacion

## Assumptions

- el endpoint OIDC login de Infisical es `/api/v1/auth/oidc-auth/login`
- `INFISICAL_IDENTITY_ID`, `INFISICAL_PROJECT_SLUG`, `INFISICAL_ENV_SLUG` y `INFISICAL_SECRET_PATH` existen como GitHub Variables
- el proyecto usa Infisical Cloud salvo que se indique un dominio distinto al ejecutar el workflow

## Steps

1. Crear `.github/workflows/debug-infisical-oidc.yml`.
2. Validar variables requeridas y solicitar el JWT OIDC desde GitHub.
3. Decodificar y mostrar claims/metadatos seguros del JWT.
4. Probar login directo contra Infisical y luego ejecutar `Infisical/secrets-action`.
5. Leer la ruta de secretos desde GitHub Variables y aplicarla en todos los workflows.
6. Documentar uso y troubleshooting.

## Validation

- revisar sintaxis YAML del workflow nuevo
- revisar que la documentacion refleje inputs, variables y criterios de diagnostico
- inspeccionar diff final

## Risks

- imprimir accidentalmente el JWT completo o tokens de acceso
- asumir un dominio de Infisical incorrecto en entornos self-hosted
- considerar valido el OIDC aunque el workflow tenga acceso a identidad pero no a los secretos esperados
