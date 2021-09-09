# Docker Compose Apps :whale2

Dockers para ambientes de Desarrollo / Dockers for development environment

## mysql.yml

MariaDB 10.5, Mysql 5.7 y PhpMyAdmin en version latest con theme darkwolf ademas de montar el archivo *config.user.inc.php*, usuario y password de BD seteados en *root / root*, persintencia de data de la base de datos. Archivos my.cnf y php-phpmyadmin.ini para configuraciones se copia al crear la imagen.

### Servicios

- mariadb
- mysql
- phpmyadmin

### Comando

```bash
docker-compose -f mysql.yml up -d
```

## mongo.yml

Mongo y Mongo Express en version latest, usuario y password de BD seteados en *root / root*, persintencia de data de la base de datos. Mongo Express con Auth seteada con *admin / admin*

### Servicios

- mongo
- mongo-express

### Comando

```bash
docker-compose -f mongo.yml up -d
```

## laravel.yml

Nginx latest y php-fpm 7.4 mapea una carpeta con un proyecto laravel

### Servicios

- nginx
- php-fpm

### Comando

```bash
docker-compose -f laravel.yml up -d`
```

## node.yml

node:14-alpine, mapea una carpeta con un proyecto node, realiza el npm install y deja el proyecto listo para deploy

### Servicios

- node

### Comando

```bash
docker-compose -f node.yml up -d`
```

## php_5.yml

Nginx alpine latest y php-fpm 5.6, mapea una carpeta con un proyecto php

### Servicios

- nginx
- php-fpm

### Comando

```bash
docker network create sonarnet --subnet 172.24.24.0/24
docker-compose -f php_5.yml up -d
```

## sonarqube.yml

SonarQube LTS Community, Sonar Scanner Cli Latest y BD PostgreSQL 12 para persistencia de datos de configuracion, logs y data con persistencia en las carpetas correspondientes de logs/sonarqube y data/sonarqube, al momento de levantar la imagen de sonarqube posiblemente se tenga que ampliar la memoria del servicio de elastic dentro del contenedor, en windows teniendo la consola WSL y Docker Desktop correr el siguiente comando

```bash
wsl -d docker-desktop
```

y luego

```bash
sysctl -w vm.max_map_count=262144
```

Reiniciar el docker y esperar a que levante, para ingresar via web **user:** admin, **password:** admin, el primer inicio solicitara cambio de clave, este docker-compose esta hecho de manera que todos los parametros para utilizar el Sonar Scanner esten parametrizados en el archivo **sonar-project.properties**, los campos obligatorios son: sonar.projectKey, sonar.host.url, sonar.login. Para obtener el projectKey y login primero se debe ingresar via web a SonarQube y configurar un proyecto, al terminar nos indicara cuales son los valores y estos los parametrizaremos en el archivo de **sonar-project.properties**, para obtener **sonar.host.url** solo basta con hacer un inspect al docker del SonarQube para obtener la ip con que se levanto el contenedor y esta es la que se colocara en ese parametro. Ejemplo de archivo:

> sonar.projectKey=my-project-name
>
> sonar.projectName=my-project-name
>
> sonar.projectVersion=1.0
>
> sonar.qualitygate.wait=true
>
> sonar.sources=src
>
> sonar.host.url=<http://172.18.0.2:9000>
>
> sonar.login=61974267fee051acaf8a98e0bb93b5ea595e33ab

</p>

### Servicios

- sonarqube
- sonardb
- sonar-scanner

### Comando

Ejecutar el siguiente comando para hacer pull de todas las imagenes

```bash
docker-compose -f sonarqube.yml up -d
```

Luego el siguiente comando para ejecutar el analisis una vez se ha configurado un proyecto dentro del Sonar

```bash
docker run --rm  --network=host -v path/to/folder:/usr/src sonarsource/sonar-scanner-cli -X
```

**Nota:** En caso de no poder acceder via Web por tener un VPN Ver [Misc Dockers](#dockers)

## .Env

Configuraciones de usuario y password de la base de datos, ips de containers y puertos. Rutas de proyectos para montar. Copiar .env.example a .env

## Comandos Adicionales

Mostrar containers con Ips:

```bash
docker inspect -f '{{.Name}} - {{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' (docker ps -aq)
```

## Misc

### Dockers

Hay casos que al momento de levantar los dockers estando dentro de una VPN no se pueden acceder, esto es por tema del Network virtual que crear docker para los contenedores, este error solamente se me ha presentado para el SonarQube, se soluciona creando primero una red antes de iniciar la VPN, Ver: [Error Docker VPN](https://stackoverflow.com/questions/45692255/how-make-openvpn-work-with-docker/50948930#50948930 "Implementar en el docker-compose").
