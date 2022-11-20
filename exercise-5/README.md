# Ejercicio 5
## Consigna
Investigar que hacen y para que se usan los siguientes comandos dentro de un Dockerfile:

* HEALTHCHECK
* ONBUILD
* VOLUME

Escribir la respuesta en el repositorio personal en ejercicio05/README.md, entregar el link director al archivo.

## Desarrollo
### `HEALTHCHECK`
`HEALTHCHECK` sirve para establecer pruebas para evaluar la salud de la imagen. A través de esta directiva se indican comandos para obtener la salud de la aplicación a correr en la imagen. Resulta útil si no basta con saber si la aplicación está corriendo o no para saber si está funcionando bien. Las directivas aquí indicadas se incluyen en la metadata de la imagen y se corren posteriormente. 

Hay dos valores posibles para `HEALTHCHECK`: `HEALTHCHECK [OPTIONS] CMD command`, que establece un comando a correr dentro de la imagen para verificar la salud de la misma (ya sea de consola o un exec de Docker) o `HEALTHCHECK NONE`, que desactiva las pruebas heredadas de la imagen base.

Existe una serie de argumentos para indicar cómo se debe evaluar la salud:
- **--interval=DURATION (default: 30s):** define el intervalo entre pruebas. Las pruebas se corren al ejecutar la imagen y cada intervalos configurados por este parámetro.
- **--timeout=DURATION (default: 30s):**  define el tiempo de espera límite de respuesta para considerar  fallida la prueba. Si el comando de prueba tarda más en ejecutarse que este tiempo, se considerará que la prueba falló.
- **--start-period=DURATION (default: 0s):** define cuánto después de la ejecución de la imagen debe realizarse la primera prueba. Resulta útil si la aplicación tarda un tiempo en llegar a su estado de operación normal.
- **--retries=N (default: 3):** define cuántos fallos consecutivos se tolerarán antes de declarar que la imagen no está sana.

### `VOLUME`
`VOLUME` sirve para indicar que debe montarse un volumen externo en cierto directorio de la imagen. Este directorio tiene que ser no-existente o estar vacío. Todas las operaciones que se realicen sobre este directorio, por ejemplo instrucciones `ADD` o `COPY`, deben realizarse *antes* de la declaración del volumen o serán ignoradas.

`VOLUME` recibe texto plano con uno o más argumentos (`VOLUME /var/log /opt/app`) o un arreglo JSON (`VOLUME ["/var/log/"]`).

Al correr la imagen construida a partir del Dockerfile, se crearán puntos de montaje en las ubicaciones señaladas por esta directiva y se ejecutarán sobre estos todos los comandos de construcción que se encuentren antes de la misma.

### `ONBUILD`
`ONBUILD` sirve para indicar uno o más comandos de construcción de Docker que deben correrse cuando la imagen a construir sea usada como base en otro Dockerfile. Es decir, estas directivas se incluirán en la metadata de la imagen y serán ejecutadas no durante su construcción, sino durante la construcción de una imagen que las herede, inmediatamente después de la directiva `FROM` del Dockerfile que las invoque.

Las directivas `ONBUILD` pueden ser inspeccionadas usando `docker inspect`, y son eliminadas tras construir la imagen "hijo": no son ejecutadas si esta última es, a su vez, usada como base de una tercera imagen.