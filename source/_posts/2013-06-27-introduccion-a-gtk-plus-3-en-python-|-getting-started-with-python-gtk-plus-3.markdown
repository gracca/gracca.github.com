---
layout: post
title: "Introducción a GTK+ 3 en Python | Getting started with Python GTK+ 3"
date: 2013-06-27 18:22
comments: true
categories: [fedora, gtk+, gtk+ 3, python, pygobject, script]
---

<img class="left" src="/images/python+gtk.png" width="156" height="162" title="Python & Gtk+ 3" >

<p>
Esta especie de tutorial de <a href="http://live.gnome.org/PyGObject">PyGObject</a> (<a href="http://www.python.org">Python</a> y <a href="http://www.gtk.org">GTK+ 3</a>) es casi una traducción literal de su <a href="http://python-gtk-3-tutorial.readthedocs.org">documentación</a>. Más que un tutorial, es el ejemplo más simple de como crear una ventana vacía. Seguidamente, extenderemos el script para agregarle un botón que realiza una determinada acción. Se necesita un conocimiento razonable del lenguaje Python, el cual dudo en tener :-)
</p>

<!-- more -->

Antes de comenzar, recomiendo los siguientes documentos para que podamos aprender un poco más sobre PyGObject:

*  [http://python-gtk-3-tutorial.readthedocs.org](http://python-gtk-3-tutorial.readthedocs.org)

*  [https://developer.gnome.org/gnome-devel-demos/stable/tutorial.py.html.en](http://developer.gnome.org/gnome-devel-demos/stable/tutorial.py.html.en)

*  [http://pfrields.fedorapeople.org/presentations/OhioLF2011/PyGObject.pdf](http://pfrields.fedorapeople.org/presentations/OhioLF2011/PyGObject.pdf)

*  [https://developer.gnome.org/gtk3/](https://developer.gnome.org/gtk3/)

Ejemplo Simple
--------------

Para comenzar, crearemos el ejemplo más simple posible, el cual consiste de una ventana vacía.

<img class="center" src="/images/pygobject_01.png" title="Ejemplo simple: ventana vacía" >

{% codeblock ejemplo_simple.py lang:python %}
#!/usr/bin/python
from gi.repository import Gtk

win = Gtk.Window()
win.connect("delete-event", Gtk.main_quit)
win.show_all()
Gtk.main()
{% endcodeblock %}

Explicaremos ahora cada línea del ejemplo.

    #!/usr/bin/python

La primera línea de todos los programas en Python debe empezar con `#!` seguido del camino al intérprete Python que queremos invocar.

    from gi.repository import Gtk

Para poder acceder a las clases y funciones de GTK+, primero debemos importar el módulo Gtk. La próxima línea crea una ventana vacía.

    win = Gtk.Window()

Seguidamente, conectamos la ventana a su evento *delete* para asegurarnos de que la aplicación termine al cliquear en la *x* de la ventana.

    win.connect("delete-event", Gtk.main_quit)

En el próximo paso mostramos la ventana.

    win.show_all()

Finalmente, iniciamos el *loop* de procesamiento de GTK+, del cual saldremos cuando la ventana sea cerrada (ver línea 5).

    Gtk.main()

Para ejecutar el programa, abrimos una terminal, cambiamos el directorio hasta donde está el archivo (al cual le llamé *ejemplo_simple.py*), y ponemos:

    $ python ejemplo_simple.py

Alternativamente, podemos darle permisos de ejecución y luego ejecutarlo:

    $ chmod +x ejemplo_simple.py
    $ ./ejemplo_simple.py

Ejemplo Extendido
-----------------

Para algo un poco más útil, aquí está la vesión en PyGObject del clásico programa *Hello World*.

<img class="center" src="/images/pygobject_02.png" title="Ejemplo extendido: ventana + botón" >

{% codeblock ejemplo_extendido.py lang:python %}
#!/usr/bin/python
from gi.repository import Gtk

class MyWindow(Gtk.Window):

    def __init__(self):
        Gtk.Window.__init__(self, title="Hello World")

        self.button = Gtk.Button(label="Click Here")
        self.button.connect("clicked", self.on_button_clicked)
        self.add(self.button)

    def on_button_clicked(self, widget):
        print "Hello World"

win = MyWindow()
win.connect("delete-event", Gtk.main_quit)
win.show_all()
Gtk.main()
{% endcodeblock %}

A diferencia del ejemplo simple, aquí creamos una sub-clase de `Gtk.Window` para definir nuestra propia clase `MyWindow`.

    class MyWindow(Gtk.Window):

En el constructor de la clase, tenemos que llamar al constructor de la super-clase. Además, le diremos que dé el valor de `Hello World` a la propiedad `title`.

    Gtk.Window.__init__(self, title="Hello World")

Las próximas tres líneas son usadas para crear un botón ([*widget*](http://es.wikipedia.org/wiki/Widget)), conectarlo a su señal `clicked`, y adicionarlo como hijo a la ventana.

    self.button = Gtk.Button(label="Click Here")
    self.button.connect("clicked", self.on_button_clicked)
    self.add(self.button)

En consecuencia, el método `on_button_clicked()` será llamado si cliqueamos en el botón.

    def on_button_clicked(self, widget):
        print "Hello World"

El último bloque, fuera de la clase, es muy similar al del ejemplo simple de más arriba, pero en lugar de crear una instancia de la cláse genérica `Gtk.Window`, creamos una instancia de `MyWindow`.

