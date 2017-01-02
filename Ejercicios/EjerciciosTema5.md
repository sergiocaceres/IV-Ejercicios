##Ejercicios Tema 5

###Ejercicio 1
**Instalar los paquetes necesarios para usar KVM. Se pueden seguir estas instrucciones. Ya lo hicimos en el primer tema, pero volver a comprobar si nuestro sistema está preparado para ejecutarlo o hay que conformarse con la paravirtualización.**

Primero tenemos que instalar los paquetes con las órdenes siguietes:
```
sudo apt-get install qemu-kvm libvirt-bin
```
Una vez hecho esto, ejecutamos la orden: sudo kvm-ok y nos devuelve el siguiente mensaje:
```
INFO: Your CPU does not support KVM extensions
KVM acceleration can NOT be used
```
Como lo veíamos en la primera práctica, el resultado es el mismo, por lo que mi sistema no soporta virtualización de KVM.

###Ejercicio 2
**1. Crear varias máquinas virtuales con algún sistema operativo libre tal como Linux o BSD. Si se quieren distribuciones que ocupen poco espacio con el objetivo principalmente de hacer pruebas se puede usar CoreOS (que sirve como soporte para Docker) GALPon Minino, hecha en Galicia para el mundo, Damn Small Linux, SliTaz (que cabe en 35 megas) y ttylinux (basado en línea de órdenes solo). **

La primera máquina virtual que he creado ha sido con la distribución SliTaz. Para ello, primero nos creamos un disco duro virtual en formato qcow2 con la siguiente orden:

```
qemu-img create -f qcow2 SliTaz.qcow2 200M
```

![Imagen1](http://i67.tinypic.com/29m3rqt.png)

Una vez hecho esto, instalamos el sistema con el fichero de almacenamiento virtual creado y la ISO que nos descargamos de la web de [SliTaz](http://mirror.switch.ch/ftp/mirror/slitaz/iso/stable/)

Una vez hecho esto, lanzamos el proceso de instalación con la siguiente orden:

```
sudo qemu-system-x86_64 -hda SliTaz.qcow2 -cdrom slitaz-4.0.iso &
```

Lo podemos ver en las siguientes imágenes

![Imagen2](http://i65.tinypic.com/296kspy.png)

![Imagen3](http://i66.tinypic.com/98hmqs.png)

Como se puede ver en la imagen anterior, se ha ejecutado automaticamente. Sino se ejecutara, bastaría con poner la siguiente orden:

```
qemu-system-x86_64 y fichero_almacenamiento_virtual
```

La otra distribución elegida ha sido GALPon Minimo, la cual me he descargado la imagen de su página [web](http://minino.galpon.org/es/descargas)

De nuevo volvemos a crear un disco duro virtual de 800M esta vez, ya que la ISO ocupa 670 MB
Lo hacemos con la orden

```
qemu-img create -f qcow2 GALPon.qcow2 800M
```

Una vez descargada la ISO solo falta instalarlo. Se realiza de la siguiente manera:
```
qemu-system-x86_64 -hda GALPon.qcow2 -cdrom minino-artabros-2.1_minimal.iso
```
Tras su instalación podemos ver que funciona correctamente

![Imagen4](http://i66.tinypic.com/33e7f5y.png)

![Imagen5](http://i66.tinypic.com/2dqsn4m.png)


**2. Hacer un ejercicio equivalente usando otro hipervisor como Xen, VirtualBox o Parallels.**

Para este ejercicio he decidido usar VirtualBox. La distribución que he elegido ha sido [ttylinux](http://osarchive.sda1.eu/ttylinux)

Descargamos la ISO de la página web mencionada anteriormente y simpemente lo lanzamos con virtualBox. 
Antes de nada, debemos cargar la ISO. Nos debería quedar así. Una vez hecho, vamos a ejecutar nuestra distribución para ver que funciona correctamente.

![Imagen6](http://i67.tinypic.com/2vhzlvm.png)

![Imagen7](http://i64.tinypic.com/fcepv.png)

###Ejercicio 4
**Crear una máquina virtual Linux con 512 megas de RAM y entorno gráfico LXDE a la que se pueda acceder mediante VNC y ssh.**

He elegido [Lubuntu](http://lubuntu.net/) ya que viene con LXDE instalado.

Para ello, realizamos los mismo pasos que hicimos en ejercicios anteriores. 
Primero creamos la partición virtual con el comando
```
qemu-img create -f qcow2 lubuntu.qcow2 2G
```

Nos descargamos la [ISO](https://help.ubuntu.com/community/Lubuntu/GetLubuntu) y la lanzamos con el comando

```
qemu-system-x86_64 -hda lubuntu.qcow2 -cdrom lubuntu-16.10-desktop-amd64.iso -m 512M
```

Aquí ya le estamos indicando que queremos que use 512M de RAM, con la opción -m. Vamos a ver que todo está funcionando:

![Imagen8](http://i67.tinypic.com/24v5wr9.png)

![Imagen9](http://i66.tinypic.com/23r0f2d.png)

Tenemos que descargar una herramienta para controlar el escritorio de la máquina de manera remota. Para ello, he elegido [Vinagre](https://help.gnome.org/users/vinagre/stable/introduction.html.es). Para instalarlo tan solo hay que poner el comando ```sudo apt-get install vinagre```

Una vez instalado, tendremos que arrancar de nuevo la máquina y ejecutaremos vinagre. Esto lo hacemos con la orden
```
qemu-system-x86_64 -hda lubuntu.qcow2 -cdrom lubuntu-16.10-desktop-amd64.iso -m 512M -vnc :1
```

Una vez lanzado, tenemos que ejecutar en otra terminal ```vinagre localhost:1``` para poder verlo de forma remota. Lo podemos ver en las siguientes imagenes:

![Imagen10](http://i64.tinypic.com/33vdn6h.png)

![Imagen11](http://i68.tinypic.com/25jkold.png)

Ahora debemos instalar en la máquina ssh con la orden ```sudo apt-get install ssh```.

Una vez instalado ssh en la máquina virtual, la arrancaremos de la siguiente manera:
```
qemu-system-x86_64 -hda lubuntu.qcow2 -cdrom lubuntu-16.10-desktop-amd64.iso -m 512M -redir tcp:8427:22
```

Con la opción -rdir le estamos indicando que el puerto 8427 de la máquina anfitriona corresponde al 22 de la virtual.

Para conectarnos tan solo debemos ejecutar ```ssh sergio@localhost -p 8427```

###Ejercicio 6
**Instalar una máquina virtual con Linux Mint para el hipervisor que tengas instalado.**

Nos descargamos la [ISO](https://www.linuxmint.com/download.php) de Linux Mint. El hipervisor que voy a utilizar será VirtualBox ya que es el que tengo instalado. Vamos a crear la máquina virtual:

![Imagen12](http://i63.tinypic.com/29bmr7b.png)

Una vez seleccionado, ya podemos ver que se inicia sin ningún problema:

![Imagen13](http://i67.tinypic.com/4lpwdw.png)