##Ejercicios Tema 3

###Ejercicio 1
**Darse de alta en algún servicio PaaS tal como Heroku, Nodejitsu, BlueMix u OpenShift.**

Me he dado de alta en [Heroku](https://www.heroku.com/)

En primer lugar rellenamos un formulario de registro:

![Imagen 1](http://i64.tinypic.com/nf0dmr.png)

Una vez hecho esto, confirmamos el registro. Debemos entrar a nuestro correo electrónico y pinchar en el enlace de confirmación

![Imagen 2](http://i66.tinypic.com/mta4cm.png)

Ya podremos acceder a la interfaz de Heroku


![Imagen 3](http://i67.tinypic.com/2ci8ifa.png)


###Ejercicio 2
**Crear una aplicación en OpenShift o en algún otro PaaS en el que se haya dado uno de alta. Realizar un despliegue de prueba usando alguno de los ejemplos.**


Hemos creado la aplicación en Heroku y dentro instalaremos Wordpress. Los pasos son los siguientes:

Instalamos heroku: 
```
sudo wget -qO- https://toolbelt.heroku.com/install-ubuntu.sh | sh
```
Una vez instalado, comprobamos que la instalación se ha realizado correctamente con 
```
heroku --version
```

Una vez realizado esto ejecutamos las siguientes ordenes:

```
git clone git://github.com/mhoofman/wordpress-heroku.git 
cd wordpress-heroku/
heroku create
```
Tras haber realizado este paso, nos pide el email y la contraseña con la que nos hemos registrado. El resultado es el siguiente:

![Imagen 4](http://i63.tinypic.com/1joldl.png)

Continuamos con las siguientes ordenes
```
heroku addons:create heroku-postgresql
```
Nos fijamos en lo que muestra la salida ya que necesitamos saberlo para insertar el comando siguiente

![Imagen 5](http://i63.tinypic.com/29vcew1.png)

Nos fijamos en lo que aparece en naranja, "postgresql-horizontal-66158". Esto es lo que pondremos en el siguiente comando
```
heroku pg:promote postgresql-horizontal-66158
git add .
git push heroku master
```

Una vez hecho los comandos anteriores, nos fijamos en la salida ya que ahi viene nuestra url:

![Imagen 6](http://i65.tinypic.com/2n9dim8.png)

Nos fijamos y nuestra url es la siguiente: 
```
https://enigmatic-dusk-18730.herokuapp.com/
```

Una vez hecho esto, entramos a esa url y completamos el idioma:

![Imagen 7](http://i66.tinypic.com/2ypdaad.png)

Una vez seleccionado el idioma, nos aparece una especie de formulario que rellenaremos:

![Imagen 8](http://i67.tinypic.com/2h5mwe8.png)

Una vez rellenado nos aparece la siguiente página

![Imagen 9](http://i66.tinypic.com/2qn7evs.png)

Ya lo tenemos listo, simplemente ponemos la url mencionada antes y nos aparece lo siguiente:

![Imagen 10](http://i67.tinypic.com/29djrbb.png)

Podemos cambiar el nombre de la url. En mi caso he puesto ejercicioiv en vez de el "enigmatic-dusk-..."

![Imagen 11](http://i67.tinypic.com/iohkpt.png)

Por lo tanto, ahora a nuestra página accederemos poniendo 
```
http://ejercicioiv.herokuapp.com/
```

Lo podemos ver en la siguiente imagen

![Imagen 12](http://i66.tinypic.com/2iw1uno.png)

###Ejercicio 3
**Realizar una app en express (o el lenguaje y marco elegido) que incluya variables como en el caso anterior.**

Este ejercicio lo he hecho con una aplicación de Python, con el framework Flask. En el uso variables para guardar usuarios mediante la ruta que nos inserta el usuario. Podemos ver el código como sería:

```
from wtforms import *
from flask import *
import sys, pydoc
from HTMLParser import HTMLParser

reload(sys)
sys.setdefaultencoding('utf-8')
app = Flask(__name__)

listaUsers = []
listaSurna = []


@app.route('/users')
def showUsers():
    return 'Lista de usuarios registrados: ' + ',\n'.join(map(str,listaUsers))

@app.route('/add/<username>')
def addUser(username):
    listaUsers.append(username)
    return 'Usuario registrado. Pruebe /users para ver los usuarios'

@app.route('/')
def index():
    form = RegistrationForm(request.form)
    return render_template('index.html', form=form)

if __name__ == '__main__':
    app.run(host='0.0.0.0',debug=True)  # 0.0.0.0 para permitir conexiones desde cualquier sitio. Ojo, peligroso en modo debug
```

Podemos ver como sería la ejecución. Primero añadimos usuario:

![Imagen 13](http://i66.tinypic.com/2r45xmu.jpg)

Ahora vemos la lista de usuarios registrados:

![Imagen 14](http://i68.tinypic.com/a9u59z.jpg)


###Ejercicio 4
**Crear pruebas para las diferentes rutas de la aplicación.**

Las pruebas las he realizado con la biblioteca unittest de Python. Comprobamos que existe un css y un documento html. Aquí podremos verlo mejor:

```
import *
from HTMLParser import HTMLParser

ini_html = 0
fin_html = 0
hay_css = 0
html_css = ""

class ComprobarEtiquetas(HTMLParser):
    def handle_starttag(self, tag, attrs):
        global ini_html
        global hay_css
        if tag=='html':
            ini_html = 1
        for attr in attrs:
            if (attr[0] == 'href' and attr[1] == '/static/style.css'):
                hay_css = 1

    def handle_endtag(self, tag):
        global fin_html
        if tag=='html':
            fin_html = 1

class TestStringMethods(unittest.TestCase):

    def test_comprobarHTML(self):
        global ini_html
        ini_html = 1
        parser = ComprobarEtiquetas()
        self.assertEqual(ini_html,1)

    def test_comprobarCSS(self):
        global hay_css
        global html_css
        hay_css = 1
        parser = ComprobarEtiquetas()
        self.assertEqual(hay_css,1)


if __name__ == '__main__':
    unittest.main()
```

Vemos la salida de ejecutar el test:

![Imagen 15](http://i63.tinypic.com/243kphd.jpg)


###Ejercicio 5
**Instalar y echar a andar tu primera aplicación en Heroku.**