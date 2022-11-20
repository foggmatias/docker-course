# Ejercicio 1
## Consigna
1. Crea una página html que tenga tu nombre
2. Ejecuta una imagen nginx (https://hub.docker.com/_/nginx) para que sirva tu página. Para esto tendrás que utilizar el comando docker run y deberás investigar la documentación de la imagen nginx para descubrir cómo especificarle el contenido que el servidor debe servir.

Ten presente que no hay una única forma de resolver este ejercicio.

> Pista: puede que tengas que utilizar docker run con la opción -v

Pon los archivos que resuelven el ejercicio y las correspondientes instrucciones en una carpeta "ejercicio01" de tu repositorio Github y entrega en el classroom el link directo a la misma.

## Desarrollo
El [Dockerfile](./Dockerfile) trae la última versión de [nginx](https://hub.docker.com/_/nginx) y copia el archivo [home.html](./home.html) para que nginx lo levante.

Para correr el contenedor, primero se construye la imagen mediante `docker build` y luego se corre usando `docker run`:
```bash
    docker build . -t mati-image
    docker run -d -P mati-image
``` 

En el `build`, se utiliza la opción `-t` para asignarle un nombre a la imagen, de modo de no tener que buscar el ID para luego correrla. En el `run`, se usan las opciones `-d` para correr en modo *detached* (en segundo plano) y `-P` para que Docker haga el ruteo de puertos de forma automática.

Al ejecutarse, nginx expone un puerto (por defecto el 80, apuntándolo al archivo HTML copiado al directorio base para web pública) y a su vez al encontrarlo, Docker lo conecta con un puerto del sistema anfitrión.
