---
layout: post
title: "Python: ndarray vs. list"
date: 2013-09-15 22:22
comments: true
categories: [fedora, python, numpy, scipy, ipython]
---

<img class="left" src="/images/python-scipy.png" width="130.8" height="107.4" title="Numpy & Scipy" >

Este fin de semana comencé a leer un libro introductorio sobre [SciPy](http://www.scipy.org/) y [NumPy](http://www.numpy.org/), al cual pueden verlo acá:

[SciPy and NumPy (Optimizing & Boosting Your Python Programming)](http://books.google.com.br/books?id=-N9ZBsjW3IIC&lpg=PP1&pg=PP1#v=onepage&q&f=false)

Voy a comentar sobre un cálculo interesante que se habla en el segundo capítulo sobre la diferencia en la eficiencia computacional entre el objeto `list` y el objeto `ndarray`.

<!-- more -->

Las operaciones sobre los elementos de una lista sólo pueden ser hechas a través de bucles iterativos, lo cual es computacionalmente ineficiente en Python. El paquete NumPy permite superar las deficiencias de las listas de Python mediante un objeto para almacenamiento de datos llamado `ndarray`.

Utilizando el comando mágico `%timeit` de [IPython](http://ipython.org/), comparamos las diferencias en velocidad de `ndarray` de NumPy versus las listas de Python al ser multiplicados por un escalar. Primero creamos un *array* que contenga 1&times;10<sup>7</sup> elementos:

    In [1]: import numpy as np
    
    In [2]: arr = np.arange(1e7)

y luego convertimos el *array* en una lista:

    In [3]: larr = arr.tolist()

En el caso de las listas, tenemos que crear una función para emular lo que `ndarray` puede hacer:

    In [4]: def list_times(alist, scalar):
      ....:     for i, val in enumerate(alist):
      ....:         alist[i] = val * scalar
      ....:     return alist

Ahora hacemos el cálculo en IPython con `%timeit`, primero multiplicando el *array* por 1.1:

    In [5]: %timeit arr * 1.1
    10 loops, best of 3: 58.9 ms per loop

y luego haciendo lo mismo con la lista, usando la función creada para ello:

    In [6]: %timeit list_times(larr, 1.1)
    1 loops, best of 3: 1.44 s per loop

Esto nos muestra que la operación con el objeto `ndarray` es ~ 25 veces más rápida que el bucle con la lista. Por lo tanto, cuando sea posible, deberemos trabajar con objetos *array* en lugar de listas.

Interesante resultado para mí que soy un aprendiz de Python! :-)
