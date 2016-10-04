##Ejercicios Tema 1

###Ejercicio 1
**Consultar en el catálogo de alguna tienda de informática el precio de un ordenador tipo servidor y calcular su coste de amortización a cuatro y siete años. [Consultar este artículo en Infoautónomos sobre el tema](http://infoautonomos.eleconomista.es/consultas-a-la-comunidad/988/)**

Para realizar este ejercicio he elegido el [Lenovo TS-440 Think Server Intel Xeon](https://www.pccomponentes.com/lenovo-ts-440-think-server-intel-xeon-v1225-e3-4gb)

El precio original de este equipo es de 679€, por lo que quitándole el IVA se nos quedaría en

``679 * 0,21 = 142,59``  calculamos cuánto es el IVA del equipo para restarselo al total

``679 - 272,79 = 536,41€`` sería el precio del equipo sin IVA

Otra forma de hacerlo sería la siguiente

``679 * 0,79 =536,41€``

####Amortización a 4 años

Para amortizarlo en un plazo de 4 años debemos amortizar cada año un 25% ya que es el máximo autorizado. Por tanto haríamos lo siguiente

``536,41 * 0,25 = 134,10€ cada año``

####Amortización a 7 años

En este caso podríamos hacer lo siguiente

- Primer y segundo año al 25% -> ``536,41 * 0,25 = 134,10(cada año) * 2(número de años) = 268,21€`` a los 2 años

- Tercer y cuarto año al 15% -> ``536,41 * 0,15 = 80,46(cada año)* 2(número de años) = 160,92€`` a los 2 años

- Quinto año al 10% -> ``536,41 * 0,10 = 53,64€`` el quinto año

- Sexto y Séptimo año al 5% -> ``536,41 * 0,05 = 26,82(cada año) * 2(número de años) = 53,64€`` a los 2 años

Por tanto, si sumamos los resultados totales nos daría el precio sin IVA -> ``268,21 + 160,92 + 53,64 + 53,64 = 536,41€``


###Ejercicio 2

**Usando las tablas de precios de servicios de alojamiento en Internet y de proveedores de servicios en la nube, comparar el coste durante un año de un ordenador con un procesador estándar (escogerlo de forma que sea el mismo tipo de procesador en los dos vendedores) y con el resto de las características similares (tamaño de disco duro equivalente a transferencia de disco duro) en el caso de que la infraestructura comprada se usa sólo el 1% o el 10% del tiempo.**

He elegido los siguientes servidores: [Servidor en la nube](https://www.axarnet.es/servidores-cloud?gclid=CjwKEAjwhdOwBRDFsYTfhvzX1hYSJAAfCUcLlhWPqpC98amsCCPtwDXgPVC9YKxml8i-kNoV4QXIQBoClyfw_wcB) y [Servidor dedicado](https://www.1and1.es/server-dedicated-tariff#server), en concreto el X8i.

Ambos tienen características parecidas: 

- CPU: 8vCPU frente a V3 8 Cores (HT) 
- Almacenamiento: 1 TB frente a 4TB
- RAM: 64 GB ambos

El precio para el servidor en la nube es de 199,95€/mes. Por lo que en un año costaría ``199,95 * 12 = 2.399,40€/año``

El precio para el servidor dedicado es de 299,99€/mes. Por lo que en un año costaría ``299,99 * 12 = 3.599,88€/año``

Una vez que tenemos esto, procedo a calcular su coste cuando se usa un 1% y un 10% del tiempo.

####Si lo usamos un 1% del tiempo

- Servidor en la nube -> ``0,01 * 2.399,40€/año = 23,994€/año``
- Servidor dedicado -> ``3.599,88€/año`` ya que se tiene que usar todo el tiempo, no existe posibilidad de usarlo un 1%

####Si lo usamos un 10% del tiempo

- Servidor en la nube -> ``0,1 * 2.399,40€/año = 239,94€/año``
- Servidor dedicado -> ``3.599,88€/año`` ya que se tiene que usar todo el tiempo, no existe posibilidad de usarlo un 10%


###Ejercicio 3

**1. ¿Qué tipo de virtualización usarías en cada caso? [Comentar en el foro](https://github.com/JJ/IV16-17/issues/1)**

Comentado en dicho foro

**2. Crear un programa simple en cualquier lenguaje interpretado para Linux, empaquetarlo con CDE y probarlo en diferentes distribuciones.**

Antes de nada nos creamos el programa en python. El script es el siguiente:

```
!#/usr/bin python

print "Prueba ejercicio 3"
```
Instalamos cde con la orden ``sudo apt-get install cde``

Una vez instalado debemos empaquetar el script que hemos realizado. Para ellos ejecutamos la siguiente orden: ``cde python ejercicio3.py``. Al hacer esto, nos genera el archivo cde.options y el directorio cde-package. 

![Imagen 1](https://github.com/sergiocaceres/IV-Ejercicios/blob/master/Ejercicios/Capturas/ejercicio3.2-1.png)

Nos situamos en la directorio donde se encuentra el fichero y probamos la ejecución 

![Imagen 2](https://github.com/sergiocaceres/IV-Ejercicios/blob/master/Ejercicios/Capturas/ejercicio3.2-2.png)


###Ejercicio 4

**Comprobar si el procesador o procesadores instalados tienen estos flags. ¿Qué modelo de procesador es? ¿Qué aparece como salida de esa orden?**

Para saber el procesador que tenemos basta con hacer un ``cat /proc/cpuinfo``. El resultado fue el siguiente: Intel(R) Core(TM) i7-4510U CPU @ 2.00GHz

Ejecutamos la orden egrep ``'^flags.*(vmx|svm)' /proc/cpuinfo``

![Imagen 3](https://github.com/sergiocaceres/IV-Ejercicios/blob/master/Ejercicios/Capturas/ejercicio4.png)

No devuelve nada, por lo que el procesador no tiene dicha funcionalidad o, en todo caso, desactivada


###Ejercicio 5

**1. Comprobar si el núcleo instalado en tu ordenador contiene este módulo del kernel usando la orden kvm-ok.**

Al usar la orden nos pide que instalemos el paquete cpu-checker. Lo instalamos con la orden ``sudo apt-get install cpu-checker``. Una vez instalado el paquete, podremos usarlo sin problema.
Ejecutamos la orden ``kvm-ok`` y nos muestra lo siguiente:


```
INFO: Your CPU does not support KVM extensions
KVM acceleration can NOT be used
```
Se puede observar que mi ordenador no contiene este módulo

**2. Instalar un hipervisor para gestionar máquinas virtuales, que más adelante se podrá usar en pruebas y ejercicios.**

Como hipervisor elegí VMware Player. Ya lo tengo instalado, pero se podría seguir este tutorial para la instalación: [Guía de instalación VMware](https://help.ubuntu.com/community/VMware/Player)