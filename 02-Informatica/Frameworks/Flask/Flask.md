## ¿Qué es?

Flask es un microframework para Python basado en Werkzeug que permite crear aplicaciones web de todo tipo rápidamente.

Tutorial revisado: https://j2logo.com/tutorial-flask-espanol/

Para este tutorial se va a desarrollar un blog en Flask que tendrá las siguientes características:

- Existirán dos tipos de usuarios: administradores e invitados.
- Un usuario administrador puede añadir, modificar y eliminar entradas del blog.
- Los usuarios invitados pueden registrarse en el blog para comentar las diferentes entradas.
- Un usuario administrador puede listar y eliminar usuarios, además de poder asignarles el rol de administrador.


Para esta aplicación, necesitamos tener instalados [[Python]] y [[Virtualvenv]]. Virtualvenv nos permite aislar nuestra aplicación junto con todas sus dependencias de otras aplicaciones Python que tengamos en nuestro sistema, de manera que las librerías de cada una de las aplicaciones no entren en conflicto.

Para instalar Flask (versión 1.X) escribimos lo siguiente en la terminal:

```bash
pip install Flask
```

De manera que dentro de nuestro entorno `venv`, se instalarán el framework y las librerías que necesite.

Podemos ver todas las dependencias de nuestra aplicación si ejecutamos el siguiente comando desde la terminal:

```bash
pip freeze
```

## Creando la Primera Aplicación Flask

Vamos a crear un nuevo fichero que llamaremos `run.py`. Después lo editamos y añadimos el siguiente código:

 ```python
 from flask import Flask
 app = Flask(__name__)
 
 @app.route(´/´)
 def hello_world():
	 return "Hello, World!"
 ``` 

Toda aplicación Flask es una instancia WSGI de la clase `Flask`. Por tanto, importamos dicha clase y creamos una instancia que en este caso he llamado  `app`. Para crear dicha instancia, debemos pasar como primer argumento el nombre del módulo o paquete de la aplicación. Para estar seguros de ello, utilizaremos la palabra reservada `__name__`. Esto es necesario para que Flask sepa, por ejemplo, donde encontrar las plantillas de nuestra aplicación o los ficheros estáticos.

Una de las características de Flask es que tendremos métodos asociados a las distintas URLs que componen nuestra aplicación. Es en estos métodos donde ocurre toda la magia y toda la lógica que queramos implementar. Dentro del patrón MVC, esta parte del código se correspondería con el controlador. Flask se encarga de hacernos transparente el cómo a partir de una petición a una URL se ejecuta finalmente nuestra rutina. Lo único que tendremos que hacer nosotros será añadir  un decorador a nuestra función. En este caso, hemos llamado a nuestra función `hello_world` que será invocada cada vez que se haga una petición a la URL raíz de nuestra aplicación.

El decorador `route` de la aplicación (app) es el encargado de decirle a Flask qué URL debe ejecutar su correspondiente función.

El nombre que le demos a nuestra función será usado para generar internamente URLs a partir de dicha función.

Finalmente, la función debe devolver la respuesta que será mostrada en el navegador del usuario.

Hay que tener cuidado con no nombrar al fichero que instancia nuestra aplicación `flask.py`, ya que entraría en conflicto con el propio Flask.

## Probando la Aplicación

Flask viene con un servidor interno que nos facilita mucho la fase de desarrollo. No debemos usar este servidor en un entorno de producción ya que no es su objetivo.

Para lanzar nuestra aplicación haciendo uso de este servidor, podemos ejecutar el comando `flask` o bien `python -m`.

Sin embargo, antes de ello debemos indicarle al servidor qué aplicación debe lanzar declarando la variable de entorno `FLASK_APP`.

Para declarar la variable `FLASK_APP`, debemos modificar el fichero `activate` de nuestro entorno [[Python]].

En Linux/Mac se encuentra en `env/bin/activate`. Al final del fichero añadimos lo siguiente:

```nano
export FLASK_APP="run.py"
```

En Windows se encuentra en `env/Scripts/activate.bat`. Al final del fichero añadimos lo siguiente:

 ```txt
 set "FLASK_APP=run.py"
 ``` 

Para que los cambios realizados se tengan en cuenta debemos salir del entorno de [[Python]] y volver a entrar. Para salir, hay que ejecutar en el terminal `deactivate`.

A continuación, volvemos a activar el entorno con `source env/bin/activate` si estamos en Linux/Mac, o `env/Scripts/activate.bat` si estamos en Windows.

Una vez que hemos definido dónde puede el servidor de Flask encontrar nuestra aplicación, lo lanzamos ejecutando `flask run` o `python -m flask run`.

Para comprobar que, efectivamente, nuestra aplicación funciona, podemos entrar al navegador y en la barra de direcciones introducir `localhost:5000`. Esto nos mostrará el mensaje `Hello World!` de nuestra función `"hello_world()`.

Por defecto, el servidor que viene en Flask está a la escucha en el puerto 5000 y solo acepta peticiones de nuestro propio ordenador.

Si queremos cambiar el puerto por cualquier motivo lo podemos hacer de dos formas distintas:

- Estableciendo la variable de entorno `FLASK_RUN_PORT` en un puerto diferente.
- Indicando el puerto al lanzar el servidor `flask run --port 6000`.

Para aceptar peticiones de otros ordenadores de nuestra red lanzaremos el servidor de la siguiente manera:

```bash
flask run --host 0.0.0.0
```

## Modo Debug

Flask viene con un modo debug que es muy útil usar mientras estamos desarrollando, ya que cada vez que hagamos un cambio en nuestro código reiniciará el servidor y no tendremos que hacerlo manualmente para que los cambios se tengan en cuenta.

Para activar el modo debug simplemente hay que añadir la variable de entorno `FLASK_ENV` y asignarle el valor  `development`.

En Linux/Mac: `export FLASK_ENV="development"`.
En Windows: `set "FLASK_ENV=development"`.

NOTA: No usar el modo debug en un entorno de producción.

Activar el modo debug hace que:

- Se active un depurador.
- Se tengan en cuenta los cambios después de guardarlos sin tener que reiniciar manualmente el servidor.
- Activar el modo debug, de manera que si se produce una excepción o error en la aplicación veremos una traza de los mismos.

## Uso de Plantillas para las Páginas HTML

### Routing

Anteriormente vimos de manera rápida cómo Flask asocia una URL con un método en nuestro código. Para ello, simplemente tenemos que añadir el decorador `route()` a la función que queramos ejecutar cuando se hace una petición a una determinada URL. En Flask, por convención, a las funciones que están asociadas a una URL se les llama "vistas".

### Creando la vista de la página home

La URL de esta página será "/", en ella se mostrará el listado de posts de nuestro blog. De momento, los posts se almacenarán en una lista en memoria.

Abrimos `run.py`, eliminamos la función `hello_world()` y añadimos el siguiente código:

```python
posts = []

@app.route("/")
def index ():
	return "{ posts}.format(len(posts))"
```

Primero creamos la variable `posts`. Esta variable es una lista que almacenará los posts que vayamos creando.

En segundo lugar creamos la función `index()`, que es la responsable de mostrar los posts de nuestro blog. Pero en esta primera aproximación, lo único que hace es mostrar en el navegador el número de posts que contiene la variable `posts`.

Además, se le ha añadido el decorador `route` junto con el parámetro `/`. Esto hará que cuando se acceda a la página principal, se ejecute la función `ìndex()`.

### Creando la vista que muestra el detalle de un post

En un aplicación web no todas las páginas tienen una URL definida de antemano, como es el caso de la página principal. Por ejemplo, en nuestro blog cada post tendrá una URL única que se generará dinámicamente. Sin embargo, no vamos a tener una vista por cada URL que se genere. Vamos a tener una única vista que se encargará de recoger un parámetro que identifique al post que queramos mostrar y, en base a dicho parámetro, recuperar el post para finalmente mostrarlo al usuario.

Para hacer esto, a una URL le podemos añadir secciones variables o parametrizadas con `<param>`. La vista recibirá `<param>` como un parámetro con ese mismo nombre. Opcionalmente se puede indicar un conversor para especificar el tipo de dicho parámetro así `<converter:param>`.

Por defecto, en Flask existen los siguientes conversores:

- string: Es el conversor por defecto. Acepta cualquier cadena que no contenga el carácter `/`.
- int: Acepta números enteros positivos.
- float: Acepta números en punto flotante positivos.
- path: Es como string pero acepta cadenas con el carácter `/`.
- uuid: Acepta cadenas con formato UUID.

NOTA: También es posible añadir tus propios conversores.

Veamos todo lo anterior en acción. Vamos a crear una vista para mostrar un post a partir del slug del título del mismo. Un slug es una cadena de carácteres alfanuméricos (más el carácter '-'), sin espacios, tildes ni signos de puntuación.

```python
@app.route("/p/<string:slug>/")
def show_post(slug):
	return "Mostrando el post {}".format(slug)
```

En esta vista hemos definido el parámetro slug en la URL y dicho parámetro se toma como argumento en la función show_post(slug). De momento, lo único que hace esta función es mostrar al usuario la parte de la URL que está parametrizada:

![[Pasted image 20260509192716.png]]

Al definir una URL acabada con el carácter '/', si el usuario accede a esa URL sin dicho carácter, Flask lo redirigirá a la URL acabada en '/'. En cambio, si la URL se define sin acabar en '/' y el usuario accede indicando la '/' al final, Flask dará un error HTTP 404.

### Creando la vista para crear/modificar un post

Piensa en la lógica de crear y modificar un post. Prácticamente lo que hay que hacer en ambos casos es lo mismo: recuperar datos de un formulario, crear un objeto post, asignarle los valores de los campos del formulario y guardar el objeto post. La única diferencia es que modificar un post supone recuperarlo previamente de la base de datos.

Es una buena práctica usar una única vista que nos valga para ambos casos, ya que no estaremos repitiendo código. En estas situaciones, lo que se suele hacer es tener dos endpoints (URLs) distintos, uno para crear un post y otro para modificarlo. Podrían ser /admin/post y /admin/post/<post_id>/, respectivamente.

¿Cómo hacemos para asociar dos URLs diferentes en una sola vista? Simplemente añadiendo dos decoradores a la misma función. En nuestro caso:

```python
@app.route("/admin/post/")
@app.route("/admin/post/<int:post_id>")
def post_form(post_id=None):
	return "post_form{}".format(post_id)
```

