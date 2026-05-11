El sistema de software de TI llamado "Docker" es la tecnología de organización de contenedores que posibilita la creación y el uso de los contenedores de Linux.

Con Docker, se puede utilizar los contenedores como máquinas virtuales muy livianas y modulares, y obtiene la flexibilidad necesaria para crearlos, implementarlos, copiarlos y trasladarlos de un entorno a otro, lo cual le permite optimizar las aplicaciones para la nube.

## ¿Cómo funciona?

La tecnología Docker utiliza el kernel de Linux y sus funciones, como los grupos de controls y los espacios de nombre, para dividir los procesos y ejecutarlos de manera independiente. El propósito de los contenedores es ejecutar varios procesos y aplicaciones por separado para que se pueda aprovechar mejor la infraestructura y, al mismo tiempo, conservar la seguridad que se obtendría con los sistemas individuales.

Las herramientas de contenedores, como Docker, proporcionan un modelo de implementación basado en imágenes. Esto permite compartir fácilmente una aplicación o un conjunto de servicios, con todas las dependencias en varios entornos.

## Imágenes Docker

Las imágenes Docker son los bloques de construcción fundamentales de los contenedores. Son plantillas inmutables, de sólo lectura, que contienen todo lo necesario para ejecutar una aplicación, incluido el sistema operativo, el código de la aplicación, el tiempo de ejecución y las dependencias.

Las imágenes se construyen utilizando un Dockerfile, que define las instrucciones para crear una imagen capa a capa.

Las imágenes pueden almacenarse y recuperarse de registros de contenedores como Docker Hub.

Aquí hay algunos comandos de ejemplo para trabajar con imágenes:

```bash
docker pull nginx
```
Obtiene la última imagen de Nginx de Docker Hub.

```bash
docker images
```
Lista todas las imágenes disponibles en la máquina local.

```bash
docker rmi nginx
```
Elimina una imagen de la máquina local.

## Contenedores Docker

Un contenedor Docker es una instancia en ejecución de una imagen Docker. Los contenedores proporcionan un entorno de ejecución aislado donde las aplicaciones pueden ejecutarse sin interferir entre sí ni con el sistema anfitrión. Cada contenedor tiene su propio sistema de archivos, red y espacio de procesos, pero comparte el núcleo anfitrión.

Los contenedores siguen un ciclo de vida sencillo que incluye su creación, inicio, parada y eliminación. Aquí hay un desglose de los comandos comunes de gestión de contenedores:

1. Crear un contenedor: `docker create` o `docker run`.
2. Poner en marcha un contenedor: `docker start`.
3. Detener un contenedor: `docker stop`.
4. Borrar un contenedor: `docker rm`.

Por ejemplo:

```bash
docker run -d -p 8080:80 nginx
```

Este comando ejecuta un contenedor Nginx en modo separado (ejecutándose en segundo plano), asignando el puerto 80 dentro del contenedor al puerto 8080 en la máquina anfitriona.

Tras ejecutar este comando, Docker extraerá la imagen de Nginx (si no está ya disponible), creará un contenedor y lo iniciará.

Para comprobar todos los contenedores en ejecución y parados:

```bash
docker ps -a
```

## Docker Hub

El Docker Hub es un servicio de registro basado en la nube para encontrar, almacenar y distribuir imágenes de contenedores. Los usuarios pueden enviar imágenes personalizadas a Docker Hub y compartirlas de forma pública o privada.

Comandos para interactuar con Docker Hub:

- `docker login`: Autenticarse en Docker Hub.
- `docker push my-image`: Sube una imagen personalizada a Docker Hub.
- `docker search ubuntu`: Busca imágenes oficiales y comunitarias.
- `docker pull ubuntu`: Descarga una imagen de Ubuntu desde Docker Hub.


