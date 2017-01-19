##Ejercicios Tema 6

###Ejercicio 1
**Instalar chef en la máquina virtual que vayamos a usar**

Para instalar Chef en una máquina virtual Ubuntu es escribir el siguiente comando
```
sudo su
curl -L https://www.opscode.com/chef/install.sh | bash
```
Con eso ya tendríamos instalado Chef en nuestra máquina virtual. Podemos verlo en la siguiente imagen:

![Imagen1](http://i66.tinypic.com/20afepw.png)


###Ejercicio 4
**Instalar una máquina virtual Debian usando Vagrant y conectar con ella.**

Para poder realizar este ejercicio primero instalamos Vagrant. Lo hacemos con la siguiente orden:
```
sudo apt-get install vagrant
```

Una vez instalado, vamos a descargarnos el archivo [vagrant_1.8.1_x86_64.deb](https://releases.hashicorp.com/vagrant/1.8.1/)

Para instalarlo hacemos lo siguiente:
```
sudo dpkg -i vagrant_1.8.1_x86_64.deb
```

Ahora descargaremos la imagen Debian con el siguiente comando:
```
vagrant box add debian https://github.com/holms/vagrant-jessie-box/releases/download/Jessie-v0.1/Debian-jessie-amd64-netboot.box
```

Podemos ver que se ha descargado correctamente en la siguiente imagen:

![Imagen4](http://i65.tinypic.com/21j4pqb.png)

Ahora ya estamos listos para lanzar Vagrant. Para ello hacemos lo siguiente:
```
vagrant init debian
vagrant up
vagrant ssh
```

La primera orden es para crearnos el fichero Vagrantfile

La segunda orden es para arrancar la máquina y por último son conectamos a ella mediante SSH


###Ejercicio 5
**Crear un script para provisionar nginx o cualquier otro servidor web que pueda ser útil para alguna otra práctica**

Añadimos al fichero Vagrantfile lo siguiente:
```
config.vm.box = "debian"
config.vm.provision "shell",
inline: "sudo apt-get update && sudo apt-get install -y nginx && sudo service nginx start"
```

Una vez hecho esto, ejecutamos la máquina con ```vagrant up``` y la provisionamos con ```vagrant provision```

Una vez hecho esto podremos conectarnos mediante SSH y nginx se habrá instalado correctamente. Para comprobarlo simplemente hay que hacer ```sudo service nginx status```
