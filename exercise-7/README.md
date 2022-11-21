# Ejercicio 7
## Consigna
> Para este ejercicio necesitas docker-compose, si estas usando Docker Desktop ya lo tienes instalado, sino deberás instalarlo aparte.

Crea un archivo llamado "docker-compose.yml" y pon dentro el contenido de este link: https://gitlab.com/-/snippets/2376003/raw/main/docker-compose.yml.

A continuación ejecuta este comando en una terminal: docker-compose up.
Espera unos minutos hasta que dejen de aparecer mensaje en la terminal. Luego navega localhost:3000 para verificar que la aplicación levantó correctamente.

Finalmente contesta:
- ¿Cuántos contenedores se están ejecutando? (pueden verlo en el archivo docker-compose.yml y también ejecutando docker ps)
- ¿Cuales son las imágenes en las que están basados los mencionados contenedores?
- ¿Puedes leer el docker-compose.yml y describir lo que hace cada una de sus lineas?
- Dado que cada contenedor corre en forma aislada ¿Cómo es posible que esos contenedores se vean entre sí?


Escribe tus respuestas ejercicio07/README.md en tu repositorio github y entrega el link directo al archivo.

## Desarrollo
Se corren los siguientes comandos para levantar los contenedores:
```bash
curl https://gitlab.com/-/snippets/2376003/raw/main/docker-compose.yml -o docker-compose.yml
docker compose up
```
- Hay dos contenedores en ejecución: `web` y `db`.
- `web` está basado en `nicopaez/jobvacancy-ruby:1.3.0` y `db` en `postgres:14.4-alpine`. 
- Las líneas sirven para lo siguiente:
    - `version` indica la versión de Compose para la que se escribe el archivo y no está relacionada con los contenedores en sí mismos.
    - `services` es la categoría que engloba a los contenedores a ejecutar. Para cada uno de ellos:
        - `image` indica la imagen en la que basar el presente contenedor. 
        - `links` enumera alias a partir de los cuales se pueden encontrar otros contenedores dentro del Compose. En este caso, la única presente es `db`, que al ser el nombre del otro contenedor, es redudante ya que, por defecto, todos los contenedores son accesibles por su nombre. Si se incluyera también, por ejemplo, `db:database`, podría accederse a db usando el alias "database". 
        - `environment` sirve para incluir variables de entorno en los contenedores.
        - `depends_on` sirve para establecer un orden entre contenedores para asegurar que se ejecuten primero los que forman parte de las dependencias de otros. 
- Los contenedores se ven entre sí porque Compose, por defecto, levanta una red y los conecta. Pueden alcanzarse y descubrirse usando sus nombres o cualquier alias que se indique bajo `links`. [Leer más](https://docs.docker.com/compose/networking/).