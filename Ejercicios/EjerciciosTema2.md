##Ejercicios Tema 2

###Ejercicio 1
**Instalar alguno de los entornos virtuales de node.js (o de cualquier otro lenguaje con el que se esté familiarizado) y, con ellos, instalar la última versión existente, la versión minor más actual de la 4.x y lo mismo para la 0.11 o alguna impar (de desarrollo).**

Primero instalamos virtualenv:

![Imagen 1](http://i64.tinypic.com/pbupy.png)

Cambiamos de versión usando el comando siguiente:
```
virtualenv -p /usr/bin/pythonVersion <directorio_donde_instalarlo>
cd <directorio_donde_esta_instalado>
source bin/activate
```
Podemos ver en las figuras siguientes una captura instalando la última versión y activando dicha versión

![Imagen 2](http://i63.tinypic.com/11jowty.png)

![Imagen 3](http://i64.tinypic.com/2ynkxv8.png)

###Ejercicio 2
**Como ejercicio, algo ligeramente diferente: una web para calificar las empresas en las que hacen prácticas los alumnos. Las acciones serían
Crear empresa
Listar calificaciones para cada empresa
crear calificación y añadirla (comprobando que la persona no la haya añadido ya)
borrar calificación (si se arrepiente o te denuncia la empresa o algo)
Hacer un ránking de empresas por calificación, por ejemplo
Crear un repositorio en GitHub para la librería y crear un pequeño programa que use algunas de sus funcionalidades.
Si se quiere hacer con cualquier otra aplicación, también es válido. Se trata de hacer una aplicación simple que se pueda hacer rápidamente con un generador de aplicaciones como los que incluyen diferentes marcos MVC. Si cuesta mucho trabajo, simplemente prepara una aplicación que puedas usar más adelante en el resto de los ejercicios.**

Para la aplicación he usado Django. La web se encuentra en este [repositorio](https://github.com/sergiocaceres/Ejercicio_Empresa_IV)

###Ejercicio 3
**Ejecutar el programa en diferentes versiones del lenguaje. ¿Funciona en todas ellas?**

Se puede observar como funciona correctamente.

![Imagen 4](http://i63.tinypic.com/11h8ck0.png)

###Ejercicio 4
**Crear una descripción del módulo usando package.json. En caso de que se trate de otro lenguaje, usar el método correspondiente.**

Al haber usado python necesitamos tener el setup.py, que es el equivalente. Usamos pip freeze para obtener las dependencias. Nos quedaría algo así

![Imagen 5](http://i64.tinypic.com/rbegxu.png)

###Ejercicio 5
**Automatizar con grunt y docco (o algún otro sistema) la generación de documentación de la librería que se cree. Previamente, por supuesto, habrá que documentar tal librería.**

Para generar la documentación en python podemos usar [epydoc](http://epydoc.sourceforge.net/). Bastaría con hacer ``` epydoc nombre_paquete ```. Se nos creará un directorio html, en el que se encuentra la documentación generada automáticamente

###Ejercicio 7

**Convertir los tests unitarios anteriores con assert a programas de test y ejecutarlos desde mocha, usando descripciones del test y del grupo de test de forma correcta. Si hasta ahora no has subido el código que has venido realizando a GitHub, es el momento de hacerlo, porque lo vas a necesitar un poco más adelante.**

En Python disponemos de del fichero test.py en el que podemos definir todos los test convenientes. Esta batería de test se lanzaría mediante la orden ```python manage.py test empresa```


###Ejercicio 8
**Haced los dos primeros pasos antes de pasar al tercero.**

Necesitamos definir un fichero .travis.yml. En mi caso el contenido es el siguiente:

```
language: python
python:
 - "2.7"

install:
 - sudo apt-get install python-dev
 - pip install --upgrade pip 
 - pip install Django 

script:
 - python manage.py test
```

Automaticamente Travis sincroniza el repositorio y comprueba si todo es correcto:

[![Build Status](https://travis-ci.org/sergiocaceres/Ejercicio_Empresa_IV.svg?branch=master)](https://travis-ci.org/sergiocaceres/Ejercicio_Empresa_IV)
![Imagen 6](http://i63.tinypic.com/311lvlh.png)