---
layout: post
title: "Firefox 26: sin íconos de carpetas | missing folder icons"
date: 2014-01-27 11:55
comments: true
categories: [fedora, firefox, íconos, carpetas]
---

<img class="left" src="/images/firefox.png" width="96" height="96" title="Firefox" >

El [Firefox](http://www.mozilla.org/es-AR/firefox/) 26 me dejó de mostrar los íconos de las carpetas en los bookmarks.

<!-- more -->

A esto lo podemos ver en la siguiente imagen (*click* para ampliar):

<a href="/images/firefox-sin-iconos.png"><img class="center" src="/images/firefox-sin-iconos.png" width="450" height="253" title="Firefox sin íconos de carpetas"></a>

La solución es muy sencilla y la encontré [acá](http://forums.fedoraforum.org/showpost.php?p=1455281&postcount=6). Se trata de agregar el siguiente código:

    @namespace url("http://www.mozilla.org/keymaster/gatekeeper/there.is.only.xul");
    menu.bookmark-item > .menu-iconic-left {
      visibility: visible;
    }

en el siguiente archivo:

    ~/.mozilla/firefox/<profile_name>/chrome/userChrome.css

Yo lo hice de esta forma (ejecutar la línea completa como usuario normal, sin el `$`), donde `<profile_name>` es el nombre del perfil de Firefox que se quiera modificar:

{% codeblock bash lang:bash %}
$ echo -e '\n@namespace url("http://www.mozilla.org/keymaster/gatekeeper/there.is.only.xul");\nmenu.bookmark-item > .menu-iconic-left {\n  visibility: visible;\n}' >> ~/.mozilla/firefox/7zqzyo2f.default/chrome/userChrome.css
{% endcodeblock %}

Espero que le sirva a alguien. Saludos!
