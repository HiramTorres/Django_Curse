# Documentación del curso Django

## Descripción

Este repositorio contiene códigos e instrucciones de como trabajar con Django, desde lo básico. 

## Instalación

Para instalar Django, se debe ejecutar el siguiente comando:

```terminal
pip install django
```
y comprobamos la versión de Django instalada:

```terminal
django-admin --version
```

## Creación de un proyecto

Para crear un proyecto en Django, se debe ejecutar el siguiente comando:

```terminal
django-admin startproject nombre_proyecto .
```
> Nota: El punto al final del comando, indica que se creará el proyecto en el directorio actual. Y no que se creará un directorio con el nombre del proyecto.

## Para ejecutar un servidor de desarrollo 

```terminal 
python manage.py runserver
```
Se ejecuta el archivo manage.py que se encuentra en el directorio del proyecto. Y se ejecuta el comando runserver.

Con el archivo manage.py, se pueden ejecutar otros comandos, como por ejemplo:

```terminal
python manage.py createsuperuser
```
> Nota: Este comando crea un usuario administrador para el proyecto.

Se pueden utulizar muchos otros comandos, para ver la lista de comandos, se debe ejecutar el siguiente comando:

```terminal
python manage.py help
```
Y todos estos para administrar el proyecto.

En la carpeta del pryecto se encuentra todo el código fuente con el que se administra el proyecto.

## Creación de una aplicación

Para crear una aplicación, se debe ejecutar el siguiente comando:

```terminal
python manage.py startapp nombre_aplicacion
```
> Nota: El nombre de la aplicación, debe ser en minúsculas y sin espacios.


En Django los proyectos se dividen en aplicaciones, y cada aplicación tiene su propia funcionalidad. Por ejemplo, una aplicación puede ser para la gestión de usuarios, otra para la gestión de productos, otra para la gestión de ventas, etc.


Una vez creada la aplicación, en el archivo views.py se importa la función django.http.HttpResponse, y se crea una función que retorna un texto.

```python
from django.http import HttpResponse

def hello(request):
    return HttpResponse("Hola mundo")
```

## Urls

En el archivo de urls.py se importa la funcion de views.py, y se crea una ruta para la función hello.

```python
from core import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('hello/', views.hello),
]
```
> Así es como se conectaría la carpeta de urls.py con la carpeta de views.py ubicada en core.

Si quisiera que se ejecutara el mensaje de principal en alguna otra ruta, se debe agregar otra ruta en el archivo urls.py.

```python
from core import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('hello/', views.hello), # Así desde el navegador se accede a la ruta http:// localhost:8000/hello/
    path('', views.hello),
]
```
> Nota: La ruta vacía, es la ruta principal.


## Modo debug

En el archivo settings.py, se encuentra la variable DEBUG, que por defecto tiene el valor False. Si se cambia a True, se activa el modo debug, y se muestra información de errores en el navegador. Se debe tener cuidado con este modo, ya que si se activa en un servidor de producción, se puede mostrar información sensible del servidor.

> Tener en cuenta que a la hora de poner el código en producción y sacarlo del estado de pruebas, se debe cambiar el valor de DEBUG a False.

## Migrate 

Para hacer una configuración correcta del código con la base de datos, se debe ejecutar el siguiente comando:

```terminal
python manage.py migrate
```
> Nota: Este comando debe ejecutarse cada vez que se modifique el código de la aplicación.


## Template tags

Una buena práctica es separar el código html de la lógica de la aplicación. Para esto se crea una carpeta llamada templates, y se crea un archivo llamado base.html, que contendrá el código html de la aplicación. Una vez creado el archivo base.html, se debe importar el archivo en el archivo views.py. Cuando ya se tenga todo esto, lo correcto sería crear tags para el código html, para que sea más fácil de leer y de modificar. Y no solo crear código html crudo en las líneas de python.


## Static files

Para poder utilizar los archivos estaticos como lo es CSS y JS, se debe crear una carpeta llamada static, y dentro de esta carpeta se crea otra llamada css, y otra llamada js. Después en el archivo de base.html que es donde se tiene el esqueleto principal de html se debe importar el archivo de css y js.

```html
{% load static %}   
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```
> Nota: El archivo style.css debe estar en la carpeta css.

## Condicionales 

Podemos utilizar condicionales en el html, para mostrar o no mostrar ciertos elementos. Por ejemplo tener alguna función en ciertas páginas y en otras no. 

```html
{% if request.path != "/"%} 
"Esto se muestra si la ruta es diferente a /"
 {% endif %}
```

## Pillow

Para trabajar con imagenes debemos instalar la libreria Pillow, para poder trabajar con imagenes. y asi poder subir imagenes a la base de datos.

```terminal
pip install Pillow
```

## Modelos

Para crear un modelo, se debe crear una clase que herede de models.Model, y se debe crear un atributo para cada campo de la tabla. Por ejemplo, si se quiere crear una tabla de usuarios, se debe crear una clase llamada User, y se debe crear un atributo para cada campo de la tabla. 

```python
from django.db import models

class Project(models.Model):
    name = models.CharField(max_length=50)
    email = models.EmailField()
    password = models.CharField(max_length=50)
```

Cuando ya se definen los modelos de la aplicación en este caso el de "Project", cada uno de los atributos de la clase, se convierte en un campo de la tabla, por esto es que se deben definir que tipo de datos son cada uno de los atributos.

Hay diferentes tipos de datos que se pueden utilizar, como lo son:

- CharField: Para campos de texto. 
    - max_length: Para definir el tamaño máximo del campo. (obligatorio)
- EmailField: Para campos de email.
- TextField: Para campos de texto largo.
- IntegerField: Para campos de números enteros.
- FloatField: Para campos de números decimales.
- DateField: Para campos de fecha.
- DateTimeField: Para campos de fecha y hora.
    - auto_now_add: Para que se guarde la fecha y hora de creación.
    - auto_now: Para que se guarde la fecha y hora de modificación.
- BooleanField: Para campos de tipo booleano.
- ImageField: Para campos de tipo imagen.
- FileField: Para campos de tipo archivo.

Entro muchos otros. 
> Se debe seleccionar el indicado para que la base de datos sepa que tipo de dato se está guardando.


## Migraciones

Para crear las migraciones de los modelos, se debe ejecutar el siguiente comando:

```terminal
python manage.py makemigrations
```

Para aplicar las migraciones, se debe ejecutar el siguiente comando:

```terminal
python manage.py migrate
```

## Admin



## Traducciones

Para que Django detecte el nombre en español de los valores asignados en ingles se debe crear una subclase dentro de la clase Projec, la cual se llame ```Meta``` para añadir metadatos


## MTV: Model Template View

Django utiliza el patrón de diseño MTV, que significa Model Template View. 


## Pylint

Pylint es una herramienta que nos permite analizar el código de python, y nos muestra los errores que tiene el código. Para instalar pylint se debe ejecutar el siguiente comando:

```terminal
pip install pylint
```

Para ejecutar pylint se debe ejecutar el siguiente comando:

```terminal
pylint nombre_del_archivo.py
```

