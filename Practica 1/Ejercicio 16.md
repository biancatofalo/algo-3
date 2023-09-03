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

Tengo mi solución greedy, $g$, que frena en $g_1, ..., g_r$, y otra solución $b$, que frena en $b_1, ..., b_r$, con $r<s$ (o sea, hace menos paradas que la solución greedy). 
Si existe $b$, $\exists$ un $i_0= \text {min }{i/1 \leq i \leq n \land b_i > a_i}$ (o sea, ${i_0}$ es la primera parada en la que $g$ carga y $b$ no). 
Quiero ver que $b$ se queda sin nafta al no cargar en $g_{i_0}$. 

Siempre hay una parada luego de $g_{i_0}$ ya que, como $r<s$, sea cual sea $i_0$, hay una parada luego de $g_{i_0}$ en la que $b$ frena. 
Si la siguiente parada a $g_{i_0}$ está en el km $x$, como el algoritmo greedy hizo que g frenara en, $g_{i_0}$, $x - g_{{i_0}-1} > k$. Ademas, sabemos que $b_{i_0} \geq x$. Así, $b_{i_0} \geq x \rightarrow b_{i_0} - g_{{i_0}-1} \geq x - g_{{i_0}-1} > k $. 

Por último, como $i_0$ es el minimo i tal que $b_{i_0} > g_{i_0}$, $b_{{i_0}-1} \leq $g_{{i_0}-1}$. Entonces, $b_{i_0} - b_{{i_0}-1} \geq  $b_{i_0} - g_{{i_0}-1} \geq b_{i_0} - g_{{i_0}-1} \geq x - g_{{i_0}-1} > k$. Así, $b_{i_0} - b_{{i_0}-1} > k$ y entonces se queda sin nafta. 
Así vemos que no podría existir $b$ y la solución greedy es óptima. 
