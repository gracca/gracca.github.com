---
layout: post
title: "Templates: plugin para Vim"
date: 2013-09-20 14:27
comments: true
categories: [fedora, vim, plugin, template]
---

<img class="left" src="/images/vim.png" width="96" height="96" title="Vim" >

Uno de mis editores de texto preferidos es [Vim](http://www.vim.org/), sobre todo cuando se trata de editar archivos en consola o bien para escribir código. Y es acá donde entra en juego este plugin para Vim llamado [*vim-template*](https://github.com/aperezdc/vim-template/), el cual nos proporciona un conjunto de plantillas para diferentes tipos de archivos.

<!-- more -->

Instalación
-----------

Primero que nada necesitamos tener Vim, al cual lo instalamos de la siguiente manera en Fedora:

    $ sudo yum install vim-enhanced

Luego descargamos el plugin:

    $ wget https://github.com/aperezdc/vim-template/archive/master.zip

y lo instalamos al mismo tiempo que lo extraemos:

    $ unzip -j master.zip 'vim-template-master/plugin/*' -d ~/.vim/plugin

    $ unzip -j master.zip 'vim-template-master/templates/*' -d ~/.vim/templates

De esta manera, ya tenemos instalado el plugin *vim-template* en `~/.vim/`.

Configuración
-------------

Dentro de las plantillas, se utilizan variables que van a ser expandidas según su valor. Estas variables también pueden ser sobreescritas, y es lo que voy a hacer ya que las que me interesan no toman un valor muy representativo.

Dentro del archivo `~/.vimrc` (lo creamos si no existe) voy a colocar las sigientes líneas que tomarán un valor diferente según cada usuario:

{% codeblock ~/.vimrc lang:bash %}
let g:license = "GPLv3+"
let g:email = "gracca[AT]gmail[DOT]com"
let g:username = "Germán A. Racca"
{% endcodeblock %}

las cuales representan la licencia del código, el email del usuario y su nombre, respectivamente.

También voy a configurar el *template* que más uso (`~/.vim/templates/template.py`), y para ello voy a sustituir todo su contenido por lo siguiente:

{% codeblock ~/.vim/templates/template.py lang:bash %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
#
# %FFILE%
#
# Copyright (C) %YEAR% %USER%
# E-Mail: <%MAIL%>
# License: %LICENSE%

%HERE%
{% endcodeblock %}

De esta forma queda configurado el plugin a mi gusto. Hay plantillas para otros lenguajes de programación también, y no necesariamente tienen que ser modificados. Uno también puede crear su propio *template* para el lenguaje que más utilice y que no esté por default en el plugin.

Utilización
-----------

Podemos usar este plugin de dos maneras diferentes. Una es creando un nuevo archivo, dándole un nombre y el sufijo de interés. En este caso, para poner en práctica las configuraciones hechas anteriormente, vamos a crear un archivo Python:

    $ vim foo.py

y cuando presionemos *enter* obtendremos lo siguiente:

<img class="center" src="/images/vim-template-01.png" title="Template para Python" >

Otra forma es abriendo Vim sin crear ningún archivo:

    $ vim

y seleccionando luego el *template* desde dentro, para C en este caso:

    :Template c

con lo cual obtendremos:

<img class="center" src="/images/vim-template-02.png" title="Template para C" >

Podemos ver más información y definición de variables en la página de [*vim-template*](https://github.com/aperezdc/vim-template/).
