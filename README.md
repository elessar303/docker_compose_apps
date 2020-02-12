# Docker Compose Apps
Dockers para ambientes de Desarrollo / Dockers for development environment

## Mysql.yml
Mysql 5.7 y PhpMyAdmin en version latest con theme fallen ademas de montar el archivo *config.user.inc.php*, usuario y password de BD seteados en *root / root*, persintencia de data de la base de datos. Archivo my.cnf para configuraciones se copia al crear la imagen.

### Servicios:
- mysql
- phpmyadmin

### Comando:
` docker-compose -f mysql.yml up -d`

## Laravel.yml
Nginx latest y php-fpm 7.2, mapea una carpeta con un proyecto laravel

### Servicios:
- nginx
- php-fpm

### Comando
` docker-compose -f laravel.yml up -d`

## .Env
Configuraciones de usuario y password de la base de datos, ips de containers y puertos
