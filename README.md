# Pasos a seguir con Docker

Primero crear un archivo Dockerfile

## Segundo: build la imagen:

```shell
docker build -t react-image .
```

## Tercero: crear un container

```shell
# Crear con normalidad
docker run -v (pwd)/src:/app/src -d -p 3000:3000 --name react-app react-image

# Para solo lectura
docker run -v (pwd)/src:/app/src:ro -d -p 3000:3000 --name react-app react-image

# Con archivo de variable de entorno
docker run --env-file ./.env -v (pwd)/src:/app/src -d -p 3000:3000 --name react-app react-image
```

Aqui podemos ver como incluimos tanto lo volumenes (-v) como el puerto(-p), para varibales de entorno (-e) y el nombre

### entrar en el contenerdor con Bash

```shell
docker exec -it react-app bash
```

## Comandos de ayuda:

```shell
# Para ver todos los contenedores
docker ps -a

# Para ver los contenedores que se estan ejecutando
docker ps

# Para eliminar un contendor.
docker rm <nombre> -f

# Para eliminar una images.
docker image rm <nombre>

# ó
docker -rmi <nombre>

# Se puede agregar variables de entorno.
-e MY_VARIABLE=variable
```

## Comandos de limpieza de imagenes

**Para el Ejemplo he utilizado Fish. Para Bash agregar $(comandos)**

```shell
# Detener todos los contenedores en ejecucioón
docker stop (docker ps -a -q)

# Para eliminar todas la imagenes
docker rmi (docker images -q)

# Para eliminar todos los contenedores
docker rm (docker ps -a -q)

# Eliminar las imágenes no tageadas dangling.
docker rmi $(docker images dangling=true -q)

# Elimina todas las imagenes con <none>
docker rmi (docker images | tail -n +2 | awk '$1 == "<none>" {print $'3'}')

# Eliminar las imágenes no tageadas dangling. Opciones docker images
docker image prune
```

## Comandos con volumenes

```shell
# Ver todos los volumenes
docker volume ls

# Ver detalles de determinado volumen
docker volume inspect nombre_volumen
```

### Eliminar volumenes

```shell
# Eliminaremos los volúmenes de contenedores que ya no existen
docker volume prune

# Para eliminar un volumen
docker volume rm nombre_volumen
```

## Trabajar con varios archivos Dockerfile

```shell
# Contruir imagen para desarrollo
docker build -f Dockerfile.dev .
```

# Trabajar con Docker-Compose

```shell

# Para contruir una imagen
docker-compose build

# Para contruir una imagen y ejecutar el archivo
docker-compose up --build

# Para ejecutar las intrucciones del archivo docker-compose.yml
docker-compose up -d

# Para destruir el container creado con docker-compose
docker-compose down

# Crear contenedor de desarrollo
docker-compose -f docker-compose.yml -f docker-compose-dev.yml up -d --build

# Crear contenedor de producción
docker-compose -f docker-compose.yml -f docker-compose-prod.yml up -d --build

```
