# Ejercicio 3
## Consigna
Investigar cuantas layers tienen las imágenes nicopaez/passwordapi-java:java8-alpine y nicopaez/passwordapi-java:java8-fabric.
¿Tienen estas dos imágenes alguna layer en común?

Crear una carpeta "ejercicio03" en tu repositorio y escribe tus respuesta en un archivo README.md dentro de esa carpeta. Entrega el link a dicho archivo.
> Pista: puedes utilizar el comando "docker inspect" o la herramienta [dive](https://github.com/wagoodman/dive).

## Desarrollo
Se corrieron los siguientes comandos, reemplazando `<imageid>` por el ID de la imagen descargada en cada caso:
```bash
docker pull nicopaez/passwordapi-java:java8-alpine 
docker inspect <imageid>

docker pull nicopaez/passwordapi-java:java8-fabric
docker inspect <imageid>
```
Para el caso de alpine, las capas detalladas son las siguientes:
```JSON
"RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:73046094a9b835e443af1a9d736fcfc11a994107500e474d0abf399499ed280c",
                "sha256:298c3bb2664fb7f8514ecdde8b76c0ca95c7c7b82eaa326a7e9661e017488164",
                "sha256:8bc7bbcd76b68a51a3b70de9f19faed58f9c0795802dbff98de584b7e7eb9c22",
                "sha256:07f83dc33f640a098b67a7587dfc42f0e91f3b21aa08a7a02e613edca4901e22"
            ]
        }
```

Para el caso de fabric, estas son las capas:
```JSON
 "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:73046094a9b835e443af1a9d736fcfc11a994107500e474d0abf399499ed280c",
                "sha256:7884dc8a73eb153770c61d327c027df411ea035bb2292a0a75373481a4b7fbd0",
                "sha256:717d137b16f996bf59af63c2abfd89b69faec166381549203c1439d6fdc6ddf2",
                "sha256:b85e653858e97c56eedb2e19e225c482cbad71fd54f90059c0da3c2dc58713cf",
                "sha256:f42a66141db68550a56f7b8c4cd9e2f0127d94accfe77e124f4b68999e9374b3",
                "sha256:ad275ed181794a5e37d0b3964e23ecedbd272a03ba26215f8d83de65e27436a3",
                "sha256:dd69ad62f09595f6c7ffa79438b9e7b3f0135a8d8d3e425c1bc37c8a70abc635",
                "sha256:8bef50a12deaffef57f54aaf2facddce8c04ea9253efe8afd33c44b7d0fc2f8e",
                "sha256:b4b541fa416f1d2f1d983b11c28cb1a91e3c09167cabb0cfd29fcdeb2239721c"
            ]
        }
```
La primera imagen tiene cuatro capas, mientras que la segunda tiene nueve. La primera capa es la misma para ambas, presumiblemente la de Java base.