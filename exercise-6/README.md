# Ejercicio 6
## Consigna
Crear un contenedor para la aplicación PasswordApi (del ejercicio 4) que esté basada en la imagen redhat-openjdk-18/openjdk18-openshift
disponible en la registry de Red Hat (https://catalog.redhat.com/software/containers/redhat-openjdk-18/openjdk18-openshift/58ada5701fbe981673cd6b10).


1. Escribe el dockerfile
2. Genera la imagen (docker build)
3. Publica la imagen en tu cuenta de Dockerhub


Pon el dockerfile en un repositorio Github en una carpeta ejercicio06. Agregar también en esa carpeta un archivo readme con el link a la imagen generada en dockerhub.
Entrega el link a la carpeta en el repositorio Github.

## Desarrollo
1. En primer lugar, se escribe el [dockerfile](./Dockerfile):
    ```Dockerfile
    FROM registry.redhat.io/redhat-openjdk-18/openjdk18-openshift
    COPY passwordapi.jar /opt/passwd_api/passwordapi.jar
    CMD ["java", "-jar", "/opt/passwd_api/passwordapi.jar"]
    ```
    - Se toma la imagen de Redhat, `redhat-openjdk-18/openjdk18-openshift`.
    - Se copia luego el binario a un directorio dentro de la imagen.
    - Finalmente, se dictan las directivas para ejecutarlo al correrla.

2. Luego, se inicia sesión en registry.redhat.io usando el usuario y contraseña provistos por Redhat para poder descargar de su repositorio la imagen, y se genera una imagen a partir del Dockerfile ejecutando el siguiente comando en el directorio del Dockerfile:
    ```bash
    docker login registry.redhat.io
    docker build -t foggmatiasbz/passwd-api:redhat .
    ```
3. Finalmente se publica la imagen a su repositorio:
    ```bash
    docker push foggmatiasbz/passwd-api:redhat
    ```

Para obtener esta imagen, basta con hacer `docker pull foggmatiasbz/passwd-api:redhat`.