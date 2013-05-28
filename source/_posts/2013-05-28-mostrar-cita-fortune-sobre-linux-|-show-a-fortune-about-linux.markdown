---
layout: post
title: "Mostrar cita (fortune) sobre Linux | Show a fortune about Linux"
date: 2013-05-28 04:43
comments: true
categories: fedora linux fortune cita bashrc 
---

Para que se nos muestre una cita ([fortune](http://linux.die.net/man/6/fortune)) cada vez que abrimos un terminal, basta instalar los siguientes programas en Fedora:

    $ sudo yum install cowsay fortune-mod

<!-- more -->

Para que la cita sea sobre Linux y además sea dicha por [Tux](http://es.wikipedia.org/wiki/Tux), hacemos lo siguiente:

    $ cd ~
    $ echo "fortune linux | cowsay -f tux" >> .bashrc

Luego abrimos un nuevo terminal y aparecerá algo como esto:

<img class="center" src="/images/fortune-linux.png" title="Cita (fortune)" >
