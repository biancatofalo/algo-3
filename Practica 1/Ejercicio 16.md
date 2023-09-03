# Ejercicio 16

## a) 
Al pasar por una estación, frena solo si no llega a la siguiente estación con la nafta actual. 

## b) 
Para demostrar esto, veo que: 
* La solución greedy es válida, o sea, que nunca se queda sin nafta:

A la primera estación llega porque arranca con el tanque lleno y $x_{1} \leq k$
Si llega a una estación, llega a la siguiente, porque si no tuviera suficiente nafta cargaría (por como construí la solución
greedy). 

* No existen soluciones con menos paradas:

Tengo mi solución greedy, g, que frena en $g_1, ..., g_r$, y otra solución b, que frena en $b_1, ..., b_r$, con r<s (o sea, hace menos paradas que la solución greedy). 
Si existe b, $\exists$ un $i_0=min{i/1 \leq i \leq n \land b_i > a_i}$ (o sea, {i_0} es la primera parada en la que g carga y b no). 
Quiero ver que b se queda sin nafta al no cargar en {i_0}. 
