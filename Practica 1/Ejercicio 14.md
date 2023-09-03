# Ejercicio 14
## a) 
Idea: Tomar k veces al máximo del conjunto. 

Demostracion de que el algoritmo greedy es correcto: tengo que ver que la solución es válida (es un subconjunto de X de tamaño k) y óptima (maximiza la suma). 

Primero veo que es válida: esto es trivial, ya que el algoritmo toma k elementos de X, entonces todos los elementos de la solución greedy son elementos del conjunto X, y tengo exactamente k elementos. 

Ahora veo que es óptima, o sea, que no hay un subconjunto de X de k elementos cuyos elementos sumados sumen más que los elementos de la solución greedy sumados: 

Tengo una solución greedy $S={S_1, ..., S_2} \subseteq X$. Quiero ver que si le saco h elementos a S y los reemplazo por h elementos (distintos a los que saco) de X, con $0 \leq h \leq k$ y $|S| + h \leq X$ (o sea, hay elementos suficientes que no esten en S para reemplazar a los que saco)  entonces la suma es menor. 

Llamamos OUT al subconjunto de S de h elementos que saco de S, y IN al subconjunto de X de h elementos que meto en S. Se que todos los elementos de IN son menores o iguales a todos los elementos de OUT (por como construí la solución greedy), entonces $$\sum_{i=1}^{h} IN_{i} \leq \sum_{i=1}^{h} OUT_{i}$$ (esto creo que debería demostrarlo por inducción). Esto implica que $$\sum_{i=1}^{h} IN_{i} - \sum_{i=1}^{h} OUT_{i} \leq 0$$
Entonces, $$\sum_{i=1}^{k} S_{i} + \sum_{i=1}^{h} IN_{i} - \sum_{i=1}^{h} OUT_{i} \leq \sum_{i=1}^{k} S_{i}$$
Así, queda demostrado que no hay un subconjunto de X de k elementos cuyos elementos sumados sumen más que los elementos de la solución greedy sumados, ya que si reemplazo 1 o mas elementos, la suma es menor. 
