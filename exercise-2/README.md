# Ejercicio 2
## Consigna
1. Descarga la imagen nicopaez/pingapp:3.0.0
2. Crear un repositorio en dockerhub
3. Sube la imagen descargada al repositorio creado
4. Crea una carpeta "ejercicio02" en tu repositorio y pon dentro de la misma un archivo README.md con el detalle de instrucciones que utilizaste para completar la tarea. 
5. Asegurate que la imagen queda publicada como pública.
6. Incluye al final de las instrucciones la sentencia docker pull exacta para descargar tu imagen.

> Pista: utilizar comandos tag, login y push

## Desarrollo
Se corrieron los siguientes comandos, reemplazando `<imageid>` por el ID de la imagen descargada:
```bash
docker pull nicopaez/pingapp:3.0.0
docker login
docker tag <imageid> foggmatiasbz/pingapp
docker push foggmatiasbz/pingapp
```
Para descargar: `docker pull foggmatiasbz/pingapp`