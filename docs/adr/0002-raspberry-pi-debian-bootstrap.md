# ADR 0002: Compatibilidad Debian para bootstrap de Raspberry Pi

## Contexto

La Raspberry Pi objetivo ejecuta Debian 13 (Trixie), mientras que los roles de
Docker y Tailscale asumían Ubuntu y el codename Noble. Los workflows remotos de
Ubuntu deben conservarse.

## Decisión

El workflow local se denomina `bootstrap-raspberry-pi.yml`. Los roles de Docker
y Tailscale detectan la distribución y el codename mediante facts de Ansible y
admiten Debian y Ubuntu. Cada distribución usa su repositorio APT oficial.

## Consecuencias

Un único conjunto de playbooks sirve a los flujos remoto Ubuntu y local Debian.
Las distribuciones fuera de Debian/Ubuntu fallan antes de modificar repositorios.
