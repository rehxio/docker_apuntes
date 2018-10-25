# Docker

## Imagenes

Las imagenes son la configuración de un sistema con las aplicaciones que queremos/necesitamos y toda la configuración que les afecta tanto al sistema como a las aplicaciones, apartir de estas imagenes podemos crear diferentes instancias, llamadas contenedores, es decir, usamos la imagen como un modelo desde el que se crea una virtualización con todo lo necesario para que nuestra aplicación funcione.

En el caso de que levantemos varios contenedores de la misma imagen, lo que hará docker será tener las librerías y configuraciones comunes una sola vez para todos los contenedores, y sólo replicará las aplicaciones que es lo que nos interesa tener varias veces.

Si se levanta un contenedor desde una imagen y queremos trabajar en este contenedor debemos ser conscientes que esta información que hay dentro del contenedor se va a perder, si queremos trabajar algo debemos hacerlo desde fuera del contenedor en la configuración, dentro del contenedor sólo deben estar las aplicaciones y su configuración añadidas mediante el archivo de configuración Dockerfile.

Se puede acceder al contenedor activo y trabajar en el para poder probar algo y ver si algo está fallando, de ese modo podemos corregirlo, pero nunca se debe dejar la corrección dentro del contenedor. Ya que al volver a levantar otra instancia de la imagen, se iniciará con la configuración que teníamos originalmente en la imagen.

## Comandos

Todos los comandos de docker están aquí: [Docker CLI][]

## Contenedores

Para ver los contenedores que hay en el equipo hay que ejecutar:

```docker ps -a```


## Modo background

Para poner ejecuciones de docker en segundo plano hay que añadir _-d_ .

```docker run -d sleep 10```

## Mapeo de puertos

En el Dockerfile hay que añadir _EXPOSE PUERTO_CONTENEDOR_ .

```-p <PUERTO_HOST>:<PUERTO_CONTENEDOR>```

## Volúmenes

Para conectar un directorio del host con el contenedor habría que añadir en el Dockerfile _VOLUME DIRECTORIO_CONTENEDOR_ .

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

_Añadir **-t** para ponerle un tag(un nombre)_

y por último levantamos un contenedor con la imagen que hemos creado:

```docker run -p 1234:80 minginx```

_Cuando se arranca una imagen añadir **--rm** para que se borre al morir, añadir **--name** para poder darle un nombre al contenedor, para que sea interactivo se añade **-it** y si se puede interactuar, se queda en espera de una acción y por último para que se ejecute en segundo plano se añade **-d**_

## Entrar en un contenedor que está corriendo

Si nos damos cuenta que nos hemos equivocado en algo y queremos corregirlo, podemos entrar dentro de un docker que esté corriendo para poder modificar lo que necesitemos usando:

```docker exec -it <NOMBRE_CONTENEDOR> bash```

Con esto estaríamos dentro del contenedor con un bash activo y ahí podríamos interactuar con el y su contenido.

## Ignorar ficheros

Se pueden ignorar ficheros usando el archivo .dockerignore e indicando el fichero o el directorio que queremos omitir de la copia, por ejemplo:

```web/password.txt```

## COPY vs ADD

**Se recomienda usar siempre _COPY_** a no ser que estemos seguros de que queremos/necesitamos hacer un _ADD_ .

### COPY

```COPY <src> <dest>```

Sólo admite copia de archivos locales en el mismo directorio que el archivo Dockerfile hacia el contenedor.

### ADD

```ADD <src> <dest>```

Además de lo que hace COPY, ADD también admite extracción de archivos comprimidos en formato .tar si se encuentran en local y soporte para que el src sea una URL.

## Docker Compose

Docker compose lo que hace es relacionar contenedores entre sí. La configuración de Docker Compose usa _yml_, por ejemplo:

```ruby
version: '3.1'
services:
    db:
    wordpress:
volumes:
    dbdata:
```

## Buenas prácticas

Usar imagenes pequeñas como Alpine en lugar de Ubuntu, esto reduce de 200mb que puede ocupar una imagen de Ubuntu a unos 6mb que podría ocupar una de Alpine.

Y siempre que se pueda usar imagenes creadas oficiales.

### IMPORTANTE

Dentro de los contenedores NO se debe guardar información, se debe almacenar en local y en el contenedor debe estar la aplicación, las librerías y la configuración de las mismas.

En la configuración del Dockerfile, como buena práctica se debe colocar arriba lo que menos se cambia y abajo lo que más se cambia, ya que lo que no cambie usará caché y ahorra tiempo al crear el contenedor.

[Docker CLI]: https://docs.docker.com/engine/reference/commandline/docker/
