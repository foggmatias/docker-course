# Ejercicio 4
## Consigna
Adjunto hay un archivo .jar que tiene la aplicación PasswordApi.
Esa aplicación es una aplicación Java que se ejecuta con el comando: java -jar passwordapi.jar. Eso levanta una webapi en el puerto 8080 (ver captura de pantalla).
Lo que se pide es generar una imagen Docker que corra esa aplicación. Más concretamente lo que hay que hacer es:
1. Escribir un dockerfile
2. Generar la imagen a partir del dockerfile ejecutando un docker build
3. Publicar la imagen en Dockerhub

Resolver el ejercicio en un directorio "ejercicio04" del repositorio personal.

Mencionar en el readme el link a la imagen publicada en dockerhub.

Entregar el link a la carpeta del repositorio github.

## Desarrollo
1. En primer lugar, se escribe el [dockerfile](./Dockerfile):
    ```Dockerfile
    FROM ibmjava:jre-alpine
    COPY passwordapi.jar /opt/passwd_api/passwordapi.jar
    CMD ["java", "-jar", "/opt/passwd_api/passwordapi.jar"]
    ```
    - Se toma una imagen que incluya el *runtime environment* de Java, es decir, lo que se necesita para correr un programa de Java, ya que contamos con el binario y no es necesario compilar. 
    - Se copia luego el binario a un directorio dentro de la imagen.
    - Finalmente, se dictan las directivas para ejecutarlo al correrla.

2. Luego, se genera una imagen a partir del Dockerfile ejecutando el siguiente comando en el directorio del Dockerfile:
    ```bash
    docker build -t foggmatiasbz/passwd-api .
    ```
3. Finalmente, se publica la imagen a su repositorio:
    ```bash
    docker push foggmatiasbz/passwd-api
    ```

Para obtener esta imagen, basta con hacer `docker pull foggmatiasbz/passwd-api` o `docker pull foggmatiasbz/passwd-api:latest`.