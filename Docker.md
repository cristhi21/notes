# Docker

## [Guia docker](https://www.busindre.com/guia_rapida_de_la_linea_de_comandos_de_docker)

### Ejecutable de la terminal en linux
### Ejecutar programas
```sh
docker exec -it <container> /bin/bash

docker run <parametros> <nombre imagen>:<version> <alias del contenedor>

# Parametros usuarios
-e variable de ambiente
-p / -P exponer puertos en la docker machine
--rm matar el contenedor despues de la ejecucion
-it entrar al contenedor de form ainteractiva
--name

# Construir nuestras propias imagenes
docker build -t <tag>:<version> <ruta del dockerfile>
```
construye la imagen mas simple posible con los comandos definidos en un dockerfile

Creando un ambiente completo

`docker-compose up -d`

Permite a partir de un docker-compose.yml construir todo un ecosistema de contenedore

