# server-bootstrap

Prepara servidores Debian o Ubuntu con usuario admin, SSH seguro, firewall,
Docker, Tailscale, Alloy y el layout base de `/srv`.

## Actions

| Action | Uso |
| --- | --- |
| `bootstrap-host.yml` | Bootstrap completo de un servidor remoto por SSH. |
| `bootstrap-raspberry-pi.yml` | Bootstrap completo de una Raspberry Pi Debian desde su runner local. |
| `debug-infisical-oidc.yml` | Comprueba OIDC y los secretos compartidos de Infisical. |

Todos los deploys obtienen secretos desde Infisical. La configuración y los
secretos necesarios están documentados en [docs/secrets-and-variables.md](docs/secrets-and-variables.md).

Validación local:

```bash
make ansible-check
```
