---
layout: post
title: "Usando vim como paginador | Using vim as pager"
date: 2013-05-31 10:22
comments: true
categories: fedora vim less bashrc
---

Uno de mis alias favoritos en mi `~/.bashrc` es uno al cual le llamo `vless` y tiene las propiedades de ser un paginador (al usar [less](http://linux.die.net/man/1/less)) con coloreado de sintaxis (al usar [vim](http://linux.die.net/man/1/vim)).

<!-- more -->

Para que el alias funcione, primero tenemos que tener instalado `vim`. Si no lo tenemos, lo hacemos de la siguiente manera:

    $ sudo yum install vim-enhanced

Luego, creamos el alias en el archivo `~/.bashrc`, abriéndolo con nuestro editor preferido y adicionando la siguiente línea:

    alias vless='/usr/share/vim/vim73/macros/less.sh'

Guardamos los cambios, cerramos el archivo, abrimos un nuevo terminal y hacemos un test para ver si funciona correctamente:

    $ vless /usr/share/vim/vim73/macros/less.sh

lo cual nos debería mostrar algo así:

<img class="center" src="/images/vless.png" title="Paginando con vless" >

