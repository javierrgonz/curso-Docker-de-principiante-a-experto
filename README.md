# curso-Docker-de-principiante-a-experto
Curso 'Docker, de principiante a experto' de Udemy https://www.udemy.com/course/docker-de-principiante-a-experto

- - -

## Introducción

![Arquitectura de Docker](./img/arquitecturaDocker.png)

### Imagenes

Las imágenes de Docker es un 'paquete' que contiene todo lo necesario para que funcione una aplicación.
Las capas que dispone son:

- **Capa 1 - `FROM`**: Un mini sistema operativo (Debian, Ubuntu...)
- **Capa 2 - `RUN`**: Qué vamos a usar del sistema operativo (Apache, etc...) usando comandos de máquina reales
- **Capa 3 - `CMD`**: Linea que ejecutamos. Esto es lo que va a levantar el servicio

![Capas](./img/capasImagenes.jpg)

Estas capas son de solo lectura (Read Only - RO), y se definen en el archivo DOCKERFILE. 
Un DOCKERFILE es un archivo de texto plano que define las distintas capas del contenedor

```
FROM centos:7						Instala centos7
RUN  yum -y install httpd			Instala apache
CMD	["apachedtl","-DFOREGROUND"]	Arranca apache en primer plano
```

Es muy importante que el servicio que arranque se quede en primer plano.

### Contenedores

Un contenedor es una capa adicional que trae una ejecución en tiempo real de las capas de la imagen

![Capas](./img/contenedorSample.jpg)

Mientras el CMD funcione, el contenedor va a funcionar. 
La diferencia es que esta nueva capa SÍ es de escritura (RW).
No obstante todos los cambios que vamos a hacer sobre la capa 4 son volátiles, por lo que las configuraciones
deberán realizarse en las imagenes (capas 1,2,3)

Un contenedor dispone: 
- De las capas inferiores de las **imagenes**
- **Volúmenes** que permiten establecer persistencia y guardar datos
- **Redes** para lograr comunicar contenedores entre sí

![Capas](./img/contenedorSample1.jpg)

## Instalacion

Instalar Docker: `Config file `/lib/systemd/system/docker.service`

<details><summary>how</summary>
<p>

```
# Instalar Docker

Config file /lib/systemd/system/docker.service

# CentOS
---------

    # Utilidades
    sudo yum install -y yum-utils device-mapper-persistent-data lvm2

    # Agregar el repo de docker
    sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

    # Instalar docker
    sudo yum install docker-ce -y
    # Iniciar el servicio

    sudo systemctl start docker
    # Iniciarlo con el sistema

    sudo systemctl enable docker
    # Agregar usuario al grupo docker 

    whoami # Saber el nombre de tu usuario
    sudo usermod -aG docker nombre_de_salida_en_whoami

    # Salir de la sesión
    exit

    # Iniciar de nuevo con el usuario y probar 
    docker run hello-world

# Fedora 
---------

# La instalación es igual que en CentOS, solo deben modificar la url del repo, porque los pasos son idénticos

    # Utilidades
    sudo yum install -y yum-utils device-mapper-persistent-data lvm2

    # Agregar el repo de docker
    sudo yum-config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo

    # Instalar docker
    sudo yum install docker-ce -y

    # Iniciarlo con el sistema
    sudo systemctl enable docker

    # Agregar usuario al grupo docker 
    whoami # Saber el nombre de tu usuario
    sudo usermod -aG docker nombre_de_salida_en_whoami

    # Salir de la sesión
    exit

    # Iniciar de nuevo con el usuario y probar 
    docker run hello-world

# Ubuntu
---------

    # Actualiza los repos
    sudo apt-get update

    # Instala utilidades
    sudo apt-get install apt-transport-https ca-certificates curl software-properties-common -y

    # Agregar el gpg 
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

    # Agregar el repo
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

    # Actualizar de nuevo
    sudo apt-get update

    # Instalar docker
    sudo apt-get install docker-ce

    # Iniciarlo con el sistema
    sudo systemctl enable docker

    # Agregar usuario al grupo docker 
    whoami # Saber el nombre de tu usuario
    sudo usermod -aG docker nombre_de_salida_en_whoami

    # Salir de la sesión
    exit

    # Iniciar de nuevo con el usuario y probar 
    docker run hello-world


# Debian
---------

    # Actualiza los repos
    sudo apt-get update

    # Instala utilidades
    sudo apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common -y

    # Agregar el gpg 
    curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

    # Agregar el repo
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

    # Actualizar de nuevo
    sudo apt-get update

    # Instalar docker
    sudo apt-get install docker-ce

    # Iniciarlo con el sistema
    sudo systemctl enable docker

    # Agregar usuario al grupo docker 
    whoami 
    
    # Saber el nombre de tu usuario
    sudo usermod -aG docker nombre_de_salida_en_whoami

    # Salir de la sesión
    exit

    # Iniciar de nuevo con el usuario y probar 
    docker run hello-world

```

</p>
</details>

