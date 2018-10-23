# Docker

## Imagenes

Si se levanta una imagen y se hacen cambios sin actualizar la imagen, al hacer un exit todo lo que hayamos hecho dentro se perderá porque no hemos guardado los cambios. Si volvemos a levantar otra imagen en otro docker (contenedor), se levantará con la imagen orginal, no con los cambios que hayamos ido haciendo a no ser que hayamos actualizado dicha imagen.

## Comandos

Todos los comandos de docker están aquí: [Docker CLI][]



## Contenedores

Para ver los contenedores que hay en el equipo hay que ejecutar:

```docker ps -a```


## Modo background

Para poner ejecuciones de docker en segundo plano hay que añadir -d

```docker run -d sleep 10```

## Mapeo de puertos

En el Dockerfile hay que añadir EXPOSE PUERTO_CONTENEDOR

```-p <PUERTO_HOST>:<PUERTO_CONTENEDOR>```

## Volúmenes

Para conectar un directorio del host con el contenedor habría que añadir en el Dockerfile VOLUME DIRECTORIO_CONTENEDOR

```-v <DIRECTORIO_HOST>:<DIRECTORIO_CONTENEDOR>```

## Eliminar

Para parar un contenedor y eliminarlo hay que ejecutar los siguientes comandos: 

```docker container stop <NOMBRE_CONTENEDOR>```
```docker container rm <NOMBRE_CONTENEDOR>```

## Crear una imagen propia

Se crea un archivo Dockerfile con todo lo que queremos que haga:

```docker
FROM ubuntu
RUN apt-get update
RUN apt-get install -y nginx
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

 y luego ejecutamos el siguiente comando:

```docker build -t minginx .```

y por último levantamos un contenedor con la imagen que hemos creado:

```docker run -p 1234:80 minginx```

## COPY vs ADD

**Se recomienda usar siempre COPY** a no ser que estemos seguros de que queremos/necesitamos hacer un ADD.

### COPY

```COPY <src> <dest>```

Sólo admite copia de archivos locales en el mismo directorio que el archivo Dockerfile hacia el contenedor

### ADD

```ADD <src> <dest>```

Además de lo que hace COPY, ADD también admite extracción de archivos comprimidos en formato .tar si se encuentran en local y soporte para que el src sea una URL


[Docker CLI]: https://docs.docker.com/engine/reference/commandline/docker/
