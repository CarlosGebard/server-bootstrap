# ADR 0003: Workflows de bootstrap completos

## Contexto

Los flujos remotos requerían ejecutar `bootstrap-host.yml` y después
`apply-runtime.yml` para completar la preparación de un servidor. La Raspberry
Pi ya aplicaba ambas fases en una sola ejecución.

## Decisión

`bootstrap-host.yml` ejecuta ahora bootstrap y baseline completo. Se elimina
`apply-runtime.yml` y se conserva un único workflow de diagnóstico OIDC que
valida los secretos compartidos de Infisical.

## Consecuencias

Cada workflow de despliegue prepara completamente su tipo de host en una sola
ejecución. Las actualizaciones posteriores del baseline remoto se ejecutan
volviendo a correr `bootstrap-host.yml`.
