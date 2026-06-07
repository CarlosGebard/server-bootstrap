# SSH Recovery Runbook

## Objetivo

Mantener acceso administrativo al host aunque `sshd` falle por crash, carga, cambios de configuracion o reglas de red.

## Politica aplicada

El bootstrap instala un override de systemd para `ssh.service`:

- reinicia el servicio si falla
- espera 5 segundos entre intentos
- limita el ciclo a 5 intentos por minuto

Antes de recargar politicas SSH, Ansible ejecuta `sshd -t`. Si la configuracion efectiva es invalida, el playbook falla antes de recargar el servicio.

El rol usa `reload` en vez de `restart` para evitar cortar sesiones activas cuando solo cambia configuracion.

## Limites

El auto-recovery no repara una configuracion SSH invalida. En ese caso systemd intentara levantar el servicio, pero `sshd` seguira fallando hasta corregir la configuracion.

El auto-recovery tampoco corrige bloqueos externos como:

- firewall del proveedor
- reglas UFW incorrectas
- bloqueo de fail2ban
- perdida de red
- disco lleno
- falta de memoria severa

## Validacion rapida

En el host:

```bash
sudo sshd -t
sudo systemctl status ssh
sudo systemctl cat ssh
sudo ss -tlnp | grep ':22'
```

Desde una maquina externa:

```bash
ssh -o BatchMode=yes -o ConnectTimeout=10 <admin_user>@<host> true
```

## Recuperacion por consola del proveedor

Si no se puede entrar por SSH:

1. entrar por consola web, serial console o rescue mode del proveedor
2. validar configuracion:

   ```bash
   sudo sshd -t
   ```

3. revisar logs:

   ```bash
   sudo journalctl -u ssh -n 100 --no-pager
   sudo journalctl -u fail2ban -n 100 --no-pager
   sudo ufw status verbose
   ```

4. corregir la causa
5. levantar SSH:

   ```bash
   sudo systemctl restart ssh
   sudo systemctl status ssh
   ```

## Operacion recomendada

Antes de cambios remotos en SSH o firewall, mantener una sesion SSH abierta y probar una segunda sesion nueva antes de cerrar la primera.

Para hosts criticos, mantener un canal break-glass independiente de OpenSSH publico, por ejemplo consola del proveedor o Tailscale SSH con ACL estricta.
