# Docker Compose Apps :whale2:
Dockers para ambientes de Desarrollo / Dockers for development environment

## databases.yml
MariaDB 10.4, Mysql 5.7 y PhpMyAdmin en version latest con theme fallen ademas de montar el archivo *config.user.inc.php*, usuario y password de BD seteados en *root / root*, persintencia de data de la base de datos. Archivo my.cnf para configuraciones se copia al crear la imagen.

### Servicios:
- mariadb
- mysql
- phpmyadmin

### Comando:
```bash
docker-compose -f databases.yml up -d
```

## laravel.yml
Nginx latest y php-fpm 7.4 mapea una carpeta con un proyecto laravel

### Servicios:
- nginx
- php-fpm

### Comando
```bash
docker-compose -f laravel.yml up -d`
```

## php_5.yml
Nginx alpine latest y php-fpm 5.6, mapea una carpeta con un proyecto php

### Servicios:
- nginx
- php-fpm

### Comando
```bash
docker-compose -f php_5.yml up -d
```

## .Env
Configuraciones de usuario y password de la base de datos, ips de containers y puertos. Copiar .env.example a .env

### Comandos Adicionales

Mostrar containers con Ips:
```bash
docker inspect -f '{{.Name}} - {{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' (docker ps -aq)
```
