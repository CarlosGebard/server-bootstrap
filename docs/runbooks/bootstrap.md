# Bootstrap Runbook

## Flujo

1. ejecutar `bootstrap-host.yml` con acceso inicial `root`
2. ejecutar `apply-runtime.yml` con usuario admin
3. entregar el host al repo de deploy correspondiente

## Contrato entregado

El host queda con:
- usuario admin operativo
- Docker y Docker Compose plugin
- Tailscale instalado
- Alloy instalado y habilitado
- layout base de `/srv/...`
