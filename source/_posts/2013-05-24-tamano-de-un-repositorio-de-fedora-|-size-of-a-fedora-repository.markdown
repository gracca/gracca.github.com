---
layout: post
title: "Tamaño de un repositorio de Fedora | Size of a Fedora repository"
date: 2013-05-24 22:09
comments: true
categories: [fedora, repositorio, repoquery, awk]
---

Para saber el tamaño total de algún repositorio que tengamos configurado en Fedora, digamos el repositorio `/etc/yum.repos.d/fedora.repo`, utilizamos el siguiente comando:

    $ repoquery --disablerepo=\* --enablerepo=fedora -qa --qf='%{SIZE}' | awk '{sum+=$1} END{printf("Total size: %d MB\n", sum/1024/1024)}'
      Total size: 33910 MB

Ese es el resultado que obtengo en mi caso usando Fedora 18. Podemos hacerlo con cualquier repositorio que aparezca en `/etc/yum.repos.d/`. Inclusive podemos poner más de uno, por ejemplo usando `--enablerepo=fedora,updates` sabremos el tamaño total de los repositorios `/etc/yum.repos.d/fedora.repo` y `/etc/yum.repos.d/fedora-updates.repo`

<!-- more -->

El comando [repoquery](http://linux.die.net/man/1/repoquery) (perteneciente al paquete `yum-utils`), junto con las opciones que le pusimos, nos lista los tamaños de todos los paquetes que contiene.

El comando [awk](http://linux.die.net/man/1/awk) en este caso va sumando todas las líneas, hasta que presentamos el valor final en megabytes (por eso la doble división al final).
