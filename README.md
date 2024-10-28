# Guia-Examen

Como Hacer un examen de nava jsjsjs

Se necesita visual studio


1.- Se Crea La Carpeta del programa
2.- Se abre la terminal y se pone --> py -3 -m venv .venv
3.- Se usa el activate --> .venv\scripts\activate.bat
4.- Para continuar se requieren de hacer algunas cosas que no especifico el profe pero son las siguientes SI ESTAS USANDO UNA COMPUTADORA DE NAVA SALTA ESTE PASO

-- Instalar las extenciones de python (El que dice extencion pack sirve)
-- Ir a --> editar variables de entorno --> Variables de entorno --> Nuevo --> Pegar: 

C:\Users\(Nombre de usuario)\AppData\Local\Programs\Python\Python312\Scripts

C:\Users\(Nombre de usuario)\AppData\Local\Programs\Python\Python312

y ahora si a regresar a lo anterior.

5.-Instalar el Pip --> python -m pip install --upgrade pip
6.-Instalar el Django --> python -m pip install django
7.-Crear el Projecto -->  django-admin startproject (Nombre) .
8.-Migrar el projecto --> python manage.py migrate
9.- Comprobación 1 de el proyecto --> python manage.py runserver
10.- Se crea la app --> python manage.py startapp (Nombre de la app) 
11.- Se crea el include en el archivo urls.py 
                  |
                  |
                  v
from django.urls import path, include

path("",include("(nombre de la app).urls"))


12.- En Settings.py se le agrega abajo de la linea 39 lo siguiente: '(nombre de la app)', y en la linea 107 se le cambia el idioma a: es-mx
13.- Apartir de ahora se trabajara en la carpeta app: y lo primero que se hace es agregar la carpeta llamada "templates".
14.- En la misma carpeta se crea un archivo HTML con cualquier nombre
15.- En "views.py" se pone lo siguiente para crear una clase que llama al html

def (Nombre de la vista)(request):
    return render(request,"(nombre del html).html")

16.-Se crea un archivo llamada "urls.py" y se inserta lo siguiente para poder ver el archivo html:

from django.urls import path
from (nombre de la app) import views
urlpatterns = [
    path("",views.(Nombre de la vista),name="views.(nombre de la vista)")
]

17.- Comprobacion 2 de el proyecto te deberia de salir lo que tiene el html ( si no checa las variables y sus nombres) --> python manage.py runserver
18.-Se crea el Super user con lo siguiente:

python manage.py createsuperuser
se le da de nombre admin y tambien admin la contraseña para testear

19.-Ahora podemos empezar a crear los modelos de la siguiente forma en el archivo que dice "models.py"

from django.db import models <---- Importa los modelos
 
# Create your models here.
class (nombre del modelo) (models.Model):

         Que tipo de dato es    la clave primaria
     (Casi siempre Charfield)     |
                      |           |
                      |           |
                      v           v     
    codigo=models.CharField(primary_key=True,max_length=6) 
    nombre=models.CharField(max_length=100) <-- el max length es para que pongas cuantos caracteres tendra
    credito=models.PositiveSmallIntegerField()

20.-Se importa el modelo hacia el "admin.py".

from django.contrib import admin
from .models import (el nombre de tu modelo)
# Register your models here.

admin.site.register((el nombre de tu modelo))

21.- despues de todo esto debes de migrar los modelos con el siguiente comando

python manage.py makemigrations
python manage.py migrate

22.-Comprobacion 3, ve a la ip /admin y intenta agregar unos datos a la tabla que creastes si te deja vas por buen camino
23.-en la sección de views.py se agregan las siguientes líneas de código para poder obtener todos los datos de la tabla y mandarla de vuelta

    from .models import (Nombre de tu modelo) <-- se agrega para importar el modelo

    Variable=(Nombre del modelo).objects.all()<-- Crea una variable que almacene todos los datos de la tabla

                                                    Esta parte se agrega al código anterior
                                                                     |
                                                                     |
                                                                     v
    return render(request,"(Nombre del html).html",{"(Variable que vas a usar para almacenar los datos)":Variable})
24.- Se crea otro html para poder extender sus contenidos a otros html, es util cuando se usa boostrapp: a continuación un bostrapp como ejemplo
                                                 |
                                                 |
                                                 |
                                                 v
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block titulo %}{% endblock %}</title>
    <!-- css de boostrap 4.3.1-->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.3.1/dist/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
</head>
<body>
<nav class="navbar navbar-expand-lg navbar-light bg-success">
    <a class="navbar-brand" href="#">Cbtis128</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
        <li class="nav-item active">
            <a class="nav-link" href="#">Inicio <span class="sr-only">(current)</span></a>
        </li>
        <li class="nav-item">
            <a class="nav-link" href="#">Profes</a>
        </li>
        </ul>
    </div>
    </nav> <!-- barra de navegacion-->
    {% block cuerpo %}{% endblock %}

<!-- los scripts boostrap-->
<script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.14.7/dist/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@4.3.1/dist/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
</body>
</html>
--------------------------------------------------------------------------------
25.-Puedes modificar el html para que puedas extenderlo de otro de esta forma:

{% extends "(html principal).html" %}

{% block titulo %}(Nom de pg){% endblock %}

{% block cuerpo %}
<h1>Prueba</h1>
{% for m  in (La variable en la que almacenastes los datos %}
    <li> {{m.campo1}}.-.-.-{{m.campo2}}.-.-.-{{m.campo3}}</li>
    {% endfor %}                   A
{% endblock %}                     |
                                   |
                                   |
26.- y pa que quede bien bonito hacemos bien las tablas de esta zona

{% extends "base.html" %}

{% block titulo %}Prueba{% endblock %}

{% block cuerpo %}
<h1>Prueba</h1>
<table class="table">
<thead>
    <tr>
      <th scope="col">Codigo</th>
      <th scope="col">Nombre</th>
      <th scope="col">Credito</th>
    </tr>
  </thead>
{% for m  in LaPrueba %}
    <tbody>
      <tr>
        <td>{{m.codigo}}</td>
        <td>{{m.nombre}}</td>
        <td>{{m.credito}}</td>
      </tr>
    </tbody>
  </table>
    {% endfor %}
{% endblock %}


27.-Para cambiar el nombre de una tabla se puede usar el siguiente comando:
class Meta:

  db_table = "producto"
  verbose_name = "Producto"
  verbose_name_plural = "Productos"


Nota para Karen:

Se puede cambiar el nombre de la base de datos en la linea 80 de settings.py pero se tendrá que
eliminar la base de datos anterior y hacer un python manage.py migrate para que vuelva a funcionar
además de que se borraran todos los datos de la anterior base de datos y se tendrán que volver a ingresar los que
añadistes en administrador
