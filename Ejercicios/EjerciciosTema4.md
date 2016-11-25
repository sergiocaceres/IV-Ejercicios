##Ejercicios Tema 4

###Ejercicio 1
**Instala LXC en tu versión de Linux favorita. Normalmente la versión en desarrollo, disponible tanto en GitHub como en el sitio web está bastante más avanzada; para evitar problemas sobre todo con las herramientas que vamos a ver más adelante, conviene que te instales la última versión y si es posible una igual o mayor a la 1.0.**

Ejecutamos la orden 
```
sudo apt-get install lxc
```
Ya lo tenemos instalado. Vamos a ver la versión

![Imagen1](http://i65.tinypic.com/30109cj.png)

Ahora vemos si está preparado para usar este tipo de tecnología y también si se ha configurado correctamente. 

Ejecutamos la orden ```lxc-checkconfig``` y vemos que está todo correcto

![Imagen2](http://i66.tinypic.com/2dqr8uc.png)

![Imagen3](http://i63.tinypic.com/29z6du9.png)

###Ejercicio 2
**Comprobar qué interfaces puente se han creado y explicarlos.**
Primero creamos el contenedor con la orden ```sudo lxc-create -t ubuntu -n una-caja ```

Una vez creada, podemos iniciarla con la orden ``` sudo lxc-start -n una-caja ```

Una vez conectado, vemos las interfaces nuevas con la orden ```ifconfig -a```

Las interfaces son:

```
lxcbr0    Link encap:Ethernet  direcciónHW fe:53:cf:78:60:3b  
          Direc. inet:10.0.3.1  Difus.:0.0.0.0  Másc:255.255.255.0
          Dirección inet6: fe80::4851:22ff:fec8:fb4b/64 Alcance:Enlace
          ACTIVO DIFUSIÓN FUNCIONANDO MULTICAST  MTU:1500  Métrica:1
          Paquetes RX:349 errores:0 perdidos:0 overruns:0 frame:0
          Paquetes TX:350 errores:0 perdidos:0 overruns:0 carrier:0
          colisiones:0 long.colaTX:0 
          Bytes RX:31320 (31.3 KB)  TX bytes:52442 (52.4 KB)

veth2BWE1Y Link encap:Ethernet  direcciónHW fe:53:cf:78:60:3b  
          Dirección inet6: fe80::fc53:cfff:fe78:603b/64 Alcance:Enlace
          ACTIVO DIFUSIÓN FUNCIONANDO MULTICAST  MTU:1500  Métrica:1
          Paquetes RX:30 errores:0 perdidos:0 overruns:0 frame:0
          Paquetes TX:45 errores:0 perdidos:0 overruns:0 carrier:0
          colisiones:0 long.colaTX:1000 
          Bytes RX:3004 (3.0 KB)  TX bytes:6695 (6.6 KB)

```

###Ejercicio 3
**1. Crear y ejecutar un contenedor basado en Debian.**

Para crear un contenedor basado en Debian usamos la siguiente orden: ```sudo lxc-create -t debian -n una-caja-debian ```

Ejecutamos el contenedor con ```sudo lxc-start -n una-caja-debian ```

**2. Crear y ejecutar un contenedor basado en otra distribución, tal como Fedora. Nota En general, crear un contenedor basado en tu distribución y otro basado en otra que no sea la tuya. Fedora, al parecer, tiene problemas si estás en Ubuntu 13.04 o superior, así que en tal caso usa cualquier otra distro. Por ejemplo, Óscar Zafra ha logrado instalar Gentoo usando un script descargado desde su sitio, como indica en este comentario en el issue.**

Voy a crear un contenedor CentOS. Para ello, necesito instalar el gestor de paquetes yum

```
sudo apt-get install yum
```

Una vez hecho esto, creamos el contenedor con la orden: ```lxc-create -t centos -n centos ```

Tenemos que establecer la contraseña con la siguiente orden :
```sudo chroot /var/lib/lxc/centos/rootfs passwd```

Una vez hecho esto, ya podremos iniciar el contenedor ```sudo lxc-start -n centos ```

###Ejercicio 4
**1. Instalar lxc-webpanel y usarlo para arrancar, parar y visualizar las máquinas virtuales que se tengan instaladas.**

Para instalar lxc-webpanel basta con seguir las instrucciones que nos encontramos en su [web](http://lxc-webpanel.github.io/install.html)

Debemos estar en modo súper-usuario. Para ello ponemos sudo su y a continuación ejecutamos la orden 
```
wget https://lxc-webpanel.github.io/tools/install.sh -O - | bash
```
A continuación pongo una captura del proceso de instalación
![Imagen 4](http://i64.tinypic.com/xokxgw.png)

Una vez instalado, ponemos en nuestro navegador la dirección http://localhost:5000/ , siendo el user: admin y la contraseña: admin. 

En la siguiente captura podremos observar las máquinas creadas. Las máquinas pueden estar corriendo, detenidas o pausadas.

![Imagen 5](http://i66.tinypic.com/2mcsopg.png)


**2. Desde el panel restringir los recursos que pueden usar: CPU shares, CPUs que se pueden usar (en sistemas multinúcleo) o cantidad de memoria.**

Simplemente seleccionamos el contenedor al que queremos restringir los recursos y lo configuramos:

![Imagen 5](http://i66.tinypic.com/2hg4e93.png)

###Ejercicio 5
**Comparar las prestaciones de un servidor web en una jaula y el mismo servidor en un contenedor. Usar nginx.**



###Ejercicio 6
**Instalar docker.**

Simplemente tenemos que ejecutar lo siguiente
```
sudo apt-get installdocker.io
```

Instalamos transport-https con el siguiente comando ```apt-get install apt-transport-https```

Tenemos que añadir la clave del repositorio Docker: ```apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9```

Faltaría añadir el repositorio a nuestra lista apt y actualizar los repositorios:

```
sh -c "echo deb https://get.docker.com/ubuntu docker main\/etc/apt/sources.list.d/docker.list"
```

Vemos que se ha instalado correctamente:

![Imagen 6](http://i64.tinypic.com/208a6op.png)

###Ejercicio 7
**1. Instalar a partir de docker una imagen alternativa de Ubuntu y alguna adicional, por ejemplo de CentOS.**

Para instalar una imagen de Ubuntu usamos ```sudo docker pull ubuntu ```

![Imagen 7](http://i67.tinypic.com/eu0rhl.png)

Comprobamos que se ha instalado correctamente con la orden ```sudo docker run ubuntu ls```

![Imagen 8](http://i67.tinypic.com/furjx3.png)

Para instalar CentOs es exactamente igual que lo que acabo de explicar, pero cambiando ubuntu por centos. Sería de la siguiente manera: ```sudo docker pull centos ```

Comprobamos también que se ha instalado correctamente con la orden  ```sudo docker run centos ls```

**2. Buscar e instalar una imagen que incluya MongoDB.**

Similar al apartado anterior. Ejecutamos ```sudo docker pull mongo``` y para ver que se ha instalado correctamente volvemos a hacer ```sudo docker run mongo ls```

Vemos ahora las imágenes que tenemos instaladas para que es correcto.

![Imagen 9](http://i65.tinypic.com/2ibyr7m.png)

###Ejercicio 8
**Crear un usuario propio e instalar nginx en el contenedor creado de esta forma.**

Lanzaremos el contenedor con la orden 
```
sudo docker run -i -t ubuntu /bin/bash
```

Ahora debemos crear el usuario y darle permisos de superusuario con las ordenes:

```
useradd -d /home/sergio -m sergio
passwd sergio
adduser sergio sudo
```

Una vez hecho esto, haremos login con nuestro usuario y la contraseña que hayamos especificado.

![Imagen 10](http://i64.tinypic.com/afcvww.png)

Para instalar nginx simplemente hacemos ``` sudo apt-get install nginx``` y vemos que funciona con la orden ```service nginx status```


###Ejercicio 9
**Crear a partir del contenedor anterior una imagen persistente con commit.**

Primero debemos localizar el id del contenedor. Para ello podemos usar la orden
```
sudo docker ps -a
```

![Imagen 11](http://i68.tinypic.com/2004f3l.png)

Una vez que ya sabemos el id, podremos realizar el commit con la orden: 
```
sudo docker commit 19198c96be48 docker-commit
```

![Imagen 12](http://i65.tinypic.com/2chnamp.png)

Ahora comprobamos que se ha creado la imagen correctamente

![Imagen 13](http://i66.tinypic.com/9k9gkg.png)

###Ejercicio 10

**Crear una imagen con las herramientas necesarias para el proyecto de la asignatura sobre un sistema operativo de tu elección.**

Lo primero que hay que hacer es crearse un archivo Dockerfile que es el que se encarga de desplegar la aplicación. El contenido de mi fichero es el siguiente:

```
FROM ubuntu:14.04
MAINTAINER Sergio Cáceres Pintor <sergiocaceres@correo.ugr.es>

#Instalamos git
RUN sudo apt-get -y update
RUN sudo apt-get install -y git

#Clonamos el repositorio
RUN sudo git clone https://github.com/sergiocaceres/IV.git

#Instalamos las herramientas de python necesarias
RUN sudo apt-get -y install python-setuptools
RUN sudo apt-get -y install python-dev
RUN sudo apt-get -y install build-essential
RUN sudo apt-get -y install python-psycopg2
RUN sudo apt-get -y install libpq-dev
RUN sudo easy_install pip
RUN sudo pip install --upgrade pip

#Instalamos los requerimientos necesarios
RUN cd IV/ && make install
```

Ahora creamos la imagen con el archivo Dockerfile:
```
docker build -t prueba .
```
![Imagen 14](http://i67.tinypic.com/35cn138.png)

Comprobamos que se ha creado:

![Imagen 15](http://i66.tinypic.com/347u0kl.png)

El "." es para que se cree en el directorio actual. Probamos su funcionamiento. Primero debemos conectarnos a la imagen creada con la orden ```sudo docker run -i -t prueba /bin/bash ```. Una vez hecho esto, ya solo queda lanzar la aplicación:

```
cd IV && make execute
```

Cuando todo esté listo, debemos saber la ipde la imagen para después introducirla en nuestro navegador y ver que funciona correctamente:

![Imagen 16](http://i63.tinypic.com/4lsj9v.png)