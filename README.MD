# Instalación de Jenkins

Para este caso, la instalación de Jenkins se realizara a través de Docker, utilizando el sistema operativo Ubuntu.

#### Requerimientos

Imagen Docker hub: https://hub.docker.com/r/jenkins/jenkins

```bash
docker pull jenkins/jenkins
```

Una vez finalice la descarga de la imagen podemos verificarla con el siguiente comando:

```bash
docker images
```

Deberíamos obtener una respuesta como la siguiente

```
REPOSITORY        TAG       IMAGE ID       CREATED         SIZE
jenkins/jenkins   latest    cd151a63c5c9   4 days ago      462MB
```

#### Instalación

Crearemos los directorios de instalación de Jenkins.

```
mkdir jenkins/jenkins-home -p
```

Navegamos a la carpeta.

```
cd jenkins
```

A continuación, crearemos el archivo docker-compose.yml, este permitirá inicializar el contenedor con la imagen de Jenkins, además de indicarle los paramentos de configuración básicos para su correcto funcionamiento.

El archivo a continuación es un fichero básico de configuración para realizar la instalación.

```
version: '3'
services:
  jenkins:
    image: jenkins/jenkins
    ports:
      - 8080:8080
      - 50000:50000
    container_name: jenkins
    volumes:
      - $PWD/jenkins_home:/var/jenkins_home
    networks:
      - net
networks:
  net:
```

> [!Importante!]
>  Este archivo debe ser nombrado "docker-compose.yml" o "compose.yml".
>  Documentación: https://docs.docker.com/compose/compose-application-model/
>  
> También, es necesario respetar el nivel de sangría y especifidad del archivo yml".
> Para mas información: https://www.freecodecamp.org/news/what-is-yaml-the-yml-file-format/

Una vez creado, podemos inicializar el contenedor con el siguiente comando:

```
docker compose up -d
```

 obtendremos la siguiente impresión.

*Creating jenkins … done*

Para validar si el contenedor se ha puesto en marcha podemos usar `docker ps`.

Una vez iniciado podremos ingresar al sitio de configuración de Jenkins a través del puerto 8080 previamente configurado.

Allí después de un breve periodo de espera destinado a la preparación de inicio del servicio, se nos presentara la siguiente pantalla solicitando credenciales de administrador.

Podemos obtenerlas digitando el siguiente comando:

```
docker logs jenkins | less
```

Less permite leer solo las ultimas líneas del registro, exactamente donde se imprime la contraseña la primera vez que iniciamos la instalación.

Una vez ingresada la contraseña podremos continuar con la creación del usuario administrador, instalación de pluggins y exploración de la interfaz.

