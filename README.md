# README

## Antes de instalar

1. Algunas gemas necesarias para Simple Project Management App **no son** compatibles con Windows. Por favor, intenta usar Linux o MacOS.
2. Esta instalación asume que has clonado este repositorio.

## Requisitos adicionales

Las siguientes dependencias son necesarias y deben ser instaladas antes de la instalación de la aplicación:

| Dependencia | Version | Instalación |
|---|---|---|
| PostgreSQL | 11 | [For Debian and related versions][5] |
| Rbenv | latest | See below |
| Ruby | 2.7.2 | See below |
| NVM | latest | [Instructions][6] |
| Node.js (with NVM) | 14 LTS | See [above][6] |
| Yarn | latest | See below |
| Redis | latest | `sudo apt install redis-server` |

Después de instalar PostgreSQL, y para poder ser utilizado desde Ruby, es necesario configurar un superusuario (además del rol `postgres`). Se recomienda utilizar el mismo nombre de usuario de su máquina. Ejecute lo siguiente:

```sh
sudo -u postgres -i
psql
CREATE ROLE <user> WITH LOGIN PASSWORD '<password>';
ALTER ROLE <user> WITH SUPERUSER;
```
