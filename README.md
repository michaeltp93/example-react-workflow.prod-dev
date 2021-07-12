# Pasos a seguir con Docker

## Primero crear un archivo Dockerfile

## Segundo build la imagen:

`docker build -t react-image .`

## tercero crear un container

`docker run -v (pwd)/src:/app/src -d -p 3000:3000 --name react-app react-image`

**Para solo lectura**
`docker run -v (pwd)/src:/app/src:ro -d -p 3000:3000 --name react-app react-image`

**Con archivo de variable de entorno**
`docker run --env-file ./.env -v (pwd)/src:/app/src -d -p 3000:3000 --name react-app react-image`

Aqui podemos ver como incluimos tanto lo volumenes (-v) como el puerto(-p), para varibales de entorno (-e) y el nombre

### entrar en el contenerdor con Bash

`docker exec -it react-app bash`

## Comandos de ayuda:

`docker ps` => para ver los contenedores que se estan ejecutando
`docker ps -a` => para ver todos los contenedores.
`docker rm <nombre> -f` => para eliminar un contendor.
`docker image rm <nombre>` o `docker -rmi <nombre>`=> para eliminar una images.
`-e MY_VARIABLE=variable` => se puede agregar variables de entorno.

## Comandos de limpieza de imagenes

Fish : `docker stop (docker ps -a -q)` => detener todos los contenedores en ejecucioón
Fish : `docker rmi (docker images -q)` => para eliminar todas la imagenes
Fish : `docker rm (docker ps -a -q)` => para eliminar todos los contenedores
Fish : `docker rmi $(docker images dangling=true -q)` => Eliminar las imágenes no tageadas dangling.
Fish : `docker rmi (docker images | tail -n +2 | awk '$1 == "<none>" {print $'3'}')` => Elimina todas las imagenes con "none"
Fish : `docker image prune` => Eliminar las imágenes no tageadas dangling. Opciones docker images

## Comandos con volumenes

```shell
# ver todos los volumenes
docker volume ls

# Ver detalles de determinado volumen
docker volume inspect nombre_volumen
```

### Eliminar volumenes

```shell
# eliminaremos los volúmenes de contenedores que ya no existen
docker volume prune

# Para eliminar un volumen
docker volume rm nombre_volumen
```

## Trabajar con varios archivos Dockerfile

`docker build -f Dockerfile.dev .`

# Trabajar con Docker-Compose

## Para contruir una imagen

`docker-compose build`

## Para contruir una imagen y ejecutar el archivo

`docker-compose up --build`

## Para ejecutar las intrucciones del archivo docker-compose.yml

`docker-compose up -d`

## Para destruir el container createdo con docker-compose

`docker-compose down`

## Crear contenedor de desarrollo

`docker-compose -f docker-compose.yml -f docker-compose-dev.yml up -d --build`

## Crear contenedor de producción

`docker-compose -f docker-compose.yml -f docker-compose-prod.yml up -d --build`
