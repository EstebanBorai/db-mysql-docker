# db-mysql-docker
> Probando MySQL con Docker

#### Requisitos
- Docker
- Git

#### Instalacion
Abir una ventana del terminal y ejecutar los siguientes comandos:

```bash
# clonar repositorio de Git
git clone https://github.com/NeyderPinzon/db-mysql-docker.git

# posicionarse en el directorio del proyecto
cd db-mysql-docker/

# NOTA: al escribir el nombre de un directorio/carpeta
# se puede utilizar la tecla TAB para autocompletar
# el nombre, los directorios suelen terminar con
# slash "/"

# construir imagenes de Docker usando el comando
# docker-compose
docker-compose up --build

# Finalmente veremos un output similar al siguiente

# seven_eleven_db | 2019-06-01T19:17:49.797404Z 0 [Warning] [MY-011810] [Server] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
# seven_eleven_db | 2019-06-01T19:17:49.822630Z 0 [System] [MY-010931] [Server] /usr/sbin/mysqld: ready for connections. Version: '8.0.16'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server - GPL.
# seven_eleven_db | 2019-06-01T19:17:49.907828Z 0 [System] [MY-011323] [Server] X Plugin ready for connections. Socket: '/var/run/mysqld/mysqlx.sock' bind-address: '::' port: 33060

# No se podra seguir utilizando esta instancia del terminal, debido a que esta sujeto al log de
# Docker, el cual esta corriendo un contenedor con nuestra instancia de MySQL.
```

#### Acceso a la base de datos en el contenedor
Para acceder al contenedor que tiene nuestra base de datos, debemos
conseguir el ID del mismo. Para ello abriremos otra ventana o instancia del terminal.

```bash
# resumen de Docker
docker ps

# Esperar una respuesta similar a esta:
CONTAINER ID        IMAGE                      COMMAND                  CREATED              STATUS              PORTS                                           NAMES
dd4c6e90778c        db-mysql-docker_database   "docker-entrypoint.s…"   About a minute ago   Up About a minute   3306/tcp, 33060/tcp, 0.0.0.0:44500->44500/tcp   seven_eleven_db

# Copiar el ID del contenedor, en este caso es dd4c6e90778c , este ID varia segun la instancia de
# Docker y cambia siempre que levantemos un contendor.

# Acceder al contendor usando docker exec
docker exec -it <el ID que copiamos> /bin/bash

# Esperar una respuesta similar a esta:
root@dd4c6e90778c:/#

# Acceder a instancia de MySQL
mysql -u root -p

# Ahora nos preguntara la password, colocar admin y luego presionar ENTER
Enter password: admin

# NOTA: Al escribir la contrasena no se mostrara ningun texto debido a que se oculta la misma
# por razones de seguridad
```

Finalmente veremos un output como el siguiente:
```bash
# Welcome to the MySQL monitor.  Commands end with ; or \g.
# Your MySQL connection id is 9
# Server version: 8.0.16 MySQL Community Server - GPL

# Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

# Oracle is a registered trademark of Oracle Corporation and/or its
# affiliates. Other names may be trademarks of their respective
# owners.

# Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

# mysql>
```
