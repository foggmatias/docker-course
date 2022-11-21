# Ejercicio 8
## Consigna
Utilizando docker compose generar una configuración para correr dos instancias de passwordapi (nicopaez/password-api) balanceadas por Nginx.

La aplicación tiene un endpoint /health que indica la ip/host de la instancia que atendió el pedido, se puede usar esto para verificar el correcto balanceo.

Poner la solución en un carpeta ejercicio08, incluyendo
- la configuración de compose
- el README.md con la forma correrlo y cualquier explicación que consideres relevante. 

Entregar el link directo a la carpeta en el repositorio.

## Desarrollo
Para completar este ejercicio, es necesario levantar tres contenedores: uno con nginx y las dos instancias de la aplicación. Para esto, se escribe el [archivo de docker compose](docker-compose.yml):
```YAML
version: '2'
services:
  nginx:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
    depends_on:
      - password_1
      - password_2
  
  password_1:
    image: nicopaez/password-api
    
  password_2:
    image: nicopaez/password-api
```

- Para el contenedor de nginx, se lo basa en la última imagen oficial y se monta un archivo de configuración, [nginx.conf](./nginx.conf), como volumen en la carpeta de configuracion de nginx dentro del contenedor. Se abre el puerto por defecto, 80, y se lo hace coincidir con el del equipo anfitrión.
- Para las aplicaciones, simplemente se generan dos contenedores basándolos en la imagen que corresponde: no hace falta abrir puertos, porque no se va a llegar directamente hacia las aplicaciones desde el equipo anfitrión.

Los contenidos del archivo [nginx.conf](./nginx.conf) son los siguientes:
```conf
events {}
http {
    upstream backend {
        server password_1:3000;
        server password_2:3000;
    }
    server {
        location / {
            proxy_pass http://backend;
        }
    }
}
```
- Se establece un upstream repartido entre dos URLs, correspondientes a ambas aplicaciones (las aplicaciones exponen el puerto 3000 en sus contenedores, y estos pueden accederse a través de la red generada por docker compose usando como dirección el nombre indicado en [el archivo de configuración de compose](./docker-compose.yml)).
- Se dirige el tráfico de la URL base al upstream.

De esta manera, se podrá acceder a cualquiera de las dos aplicaciones idénticas desde el equipo anfitrión a través de `localhost:80/` o directamente, por ser el puerto 80 el puerto por defecto, `localhost/`.