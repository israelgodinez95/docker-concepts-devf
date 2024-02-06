# docker-concepts-devf

1)  Conceptos Básicos
1.1 Explica en tus propias palabras qué es Docker y cuál es su propósito principal.
    Es una plataforma que basa su funcionamiento en contenedores los cuales pueden ejecutar aplicaciones. Estos contenedoresson ligeros y portatiles
    e incluyen todo lo necesario para ejecutar una aplicacion (codigo, bibliotecas y dependencias).
1.2 ¿Cuál es la diferencia entre una imagen y un contenedor en Docker?
    Una imagen es un elemento que inlcuye todo lo necesario para ejecutar una aplicacion. a partir de una imagen puedes crear uno o multiples
    contenedores. La diferencia es que las imagenes son estaticas, como un template que incluye lo necesario para ejecutar cierta aplicacion, mientras que los contenedores
    se pueden ejecutar.
    
2) Instalación y Configuración
2.1 Proporciona los pasos básicos para instalar Docker en un sistema operativo WINDOWS/LINUX/MAC (ELIGE UNO).
   1.- Decargar Dcoker Desktop desde el sitio web: https://www.docker.com/products/docker-desktop.
   2.- Ejecutar el archivo una vez descargado.
   3.- Seguir los pasos de instalacion (Incluida la habilitacion de Windows Subsystem for Linux).
   4.- Verificar la instalacion desde la terminal (puede ser desde git bash) con el comando docker --version.
2.2 Describe brevemente qué es Docker Hub y cómo se puede utilizar en el contexto de Docker.
   Es un lugar donde puedes encontrar imagenes de miles de aplicaciones, las puedes descagar y crear tus contenedores apartir de ellas, es un simil a lo que es github con los repositorios, pero de imagenes Docker.
   Ademas, puedes descargas la version que desees, para el sistema operativo de tu preferencia la aplicacion que necesites.
   
3) Manipulación de Contenedores
3.1 Crea un archivo Dockerfile simple que utilice una imagen base de Ubuntu y ejecute el comando
"Hello, Docker!" al iniciar el contenedor.  (PARA ESTE CASO PUEDES USAR CHATGPT O BLACKBOX IA)

Dockerfile:
        FROM ubuntu:latest
        WORKDIR /app
        COPY . ./
        CMD [ "Helolo, Docker"]
        
3.2 Explica la diferencia entre los comandos docker ps y docker ps -a. ¿Qué información proporciona cada uno?
    Ambos muestran informacion de los contenedores de nuestro sistema. La diferencia es 
    que docker ps muestra la informacion de los contenedores que se estan ejecutando, mientrs que dcoker ps -a
    muestra informacion de todos los contenedores sin importar si estan en ejecucion o no.

4)  Redes en Docker
4.1 ¿Cómo se pueden listar las redes disponibles en Docker?
    Con el comando docker network ls
4.2 Crea una red en Docker llamada "mi_red" y explica cómo asignar un contenedor a esta red al momento de iniciarlo.
    1.- Primero debemos usar el comando: docker network create my_network
    2.- Despues asigamnos el contenedor a esa red al momento de ejecutarlo de la siguiente manera: docker run -d --name nombre_de_mi_contenedor --network my_network 
        nombre_de_mi_imagen
        
5)  Persistencia de Datos
5.1 Explica la diferencia entre montar un volumen y copiar archivos directamente dentro de un contenedor.
    Que el montar un volumen te asegura persistencia de datos.
5.2 ¿Cuál es la ventaja de utilizar volúmenes en Docker para la persistencia de datos?
    Que estos datos persisten mas alla del ciclo de vida de un contenedor. Cuando el contenedor se detiene o se elimina, los datos almacenados en un 
    volumen permanenen intactos.
6) Composición con Docker Compose
6.1 ¿Qué es Docker Compose y para qué se utiliza?
   Es una herramienta de Docker para gestionar aplicaciones con multiples contenedores.
6.2 Crea un archivo docker-compose.yml para definir dos servicios:
uno que utilice la imagen de Mongo y otro que utilice la imagen de Node Version 14.
Asegúrate de especificar la red a la que pertenecerán ambos servicios.\

    version: "3"
    services:
      node-app:
        image: node:14   
        build: .
        networks:
           -mi_red
       mongo:
        image: mongo  
        build: .
        networks:
           -mi_red
     networks:
        mi_red:
           driver: bridge
   
8)  Resolución de Problemas
7.1 Imagina que un contenedor no se inicia correctamente.
 Proporciona algunos pasos que seguirías para identificar y solucionar el problema.
 Primero ejecutaria el comando docker ps para ver si existe el contenedor y se inicio correctamente, si no aparece, iria a ver en docker desktop tambien;
 Si no se encuentra, ejecutaria el comando para crearlo  docker run -p3000:3000 -d --name node-app node-app-image donde -p3000:3000 es el mapeo de los puertos a usar, node-app es el nombre de mi contenedor y node-app-imaghe es el nombre de la imagen a partir de la cual se creara y ejecutara ese contenedor
 7.2 ¿Cómo puedes acceder a la shell de un contenedor en ejecución?
    Con el comando docker exec -it {nombre del contenedor} bash
   
