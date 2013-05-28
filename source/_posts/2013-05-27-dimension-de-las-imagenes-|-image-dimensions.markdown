---
layout: post
title: "Dimensión de las imágenes | Image dimensions"
date: 2013-05-27 22:26
comments: true
categories: fedora script bash image
---

<img class="left" src="/images/resize-icon.png" >

La mayoría de las veces es necesario especificar la dimensión de las imágenes que se colocan en el blog. No sé como harán los demás, pero yo abría la imagen con algún programa e intentaba redimensionar manteniendo las proporciones, después copiaba el nuevo tamaño y listo.

<!-- more -->

Para no tener que hacer todo eso cada vez que voy a poner una imagen en el blog, escribí el siguiente script de bash, el cual es muy simple y necesita de [ImageMagick](http://www.imagemagick.org) instalado en el sistema para que funcione:

{% codeblock imgdim lang:bash %}
#!/usr/bin/env bash

# Author: Germán A. Racca (skytux)
# E-Mail: <gracca[AT]gmail[DOT]com>
# License: GPLv3+

IMAGE=$1
RATIO=$2

OUT=$(identify -format "%[fx:w*($RATIO/100)] %[fx:h*($RATIO/100)]" $IMAGE)

echo -e "$IMAGE: \033[1mwidth\033[0m and \033[1mheight\033[0m at \033[1m$RATIO%\033[0m -> \033[1m$OUT\033[0m"
{% endcodeblock %}

El script mantiene las proporciones y funciona especificando el nombre de la imagen y el tamaño en porcentaje (usando 100 nos da el tamaño real):

<img class="center" src="/images/ejemplo-imgdim.png" title="Ejemplo de uso" >
