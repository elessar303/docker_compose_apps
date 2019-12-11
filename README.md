# Docker Compose Apps
Dockers para ambientes de Desarrollo / Dockers for development environment

## Mysql.yml
Mysql 5.7 y PhpMyAdmin en version latest con theme fallen ademas de montar el archivo *config.user.inc.php*, usuario y password de BD seteados en *root / root*, persintencia de data de la base de datos.

### Servicios:
- mysql
- phpmyadmin

### Comando:
` docker-compose -f mysql.yml up -d`
