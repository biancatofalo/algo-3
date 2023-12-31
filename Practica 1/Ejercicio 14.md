# Ejercicio 14
## a) 
Idea: Tomar k veces al máximo del conjunto. 

Demostracion de que el algoritmo greedy es correcto: tengo que ver que la solución es válida (es un subconjunto de X de tamaño k) y óptima (maximiza la suma). 

Primero veo que es válida: esto es trivial, ya que el algoritmo toma k elementos de X, entonces todos los elementos de la solución greedy son elementos del conjunto X, y tengo exactamente k elementos. 

Ahora veo que es óptima, o sea, que no hay un subconjunto de X de k elementos cuyos elementos sumados sumen más que los elementos de la solución greedy sumados: 

Tengo una solución greedy $S={S_1, ..., S_2} \subseteq X$. Quiero ver que si le saco h elementos a S y los reemplazo por h elementos (distintos a los que saco) de X, con $0 \leq h \leq k$ y $|S| + h \leq X$ (o sea, hay elementos suficientes que no esten en S para reemplazar a los que saco)  entonces la suma es menor. 

Llamo OUT al subconjunto de S de h elementos que saco de S, y IN al subconjunto de X de h elementos que meto en S. Se que todos los elementos de IN son menores o iguales a todos los elementos de OUT (por como construí la solución greedy), entonces vale (demostración mas abajo) que  $$\sum_{i=1}^{h} IN_{i} \leq \sum_{i=1}^{h} OUT_{i}$$ Esto implica que $$\sum_{i=1}^{h} IN_{i} - \sum_{i=1}^{h} OUT_{i} \leq 0$$

Entonces, $$\sum_{i=1}^{k} S_{i} + \sum_{i=1}^{h} IN_{i} - \sum_{i=1}^{h} OUT_{i} \leq \sum_{i=1}^{k} S_{i}$$
Así, queda demostrado que no hay un subconjunto de X de k elementos cuyos elementos sumados sumen más que los elementos de la solución greedy sumados, ya que si reemplazo 1 o mas elementos, la suma es menor. 

------

Demostración que faltaba, sabiendo que todos los elementos de IN son menores iguales a todos los de OUT: 

Por inducción: 

P(h): si tengo h elementos en IN y h elementos en OUT, la sumatoria de los elementos de IN es menor que la de los elementos de OUT. 

Caso base: h=1
$$\sum_{i=1}^{1} IN_{i} \leq \sum_{i=1}^{1} OUT_{i} \leftrightarrow IN_{1} \leq OUT_{1}$$ y esto es verdadero. 
      
Paso inductivo: quiero ver que si $$\sum_{i=1}^{k} IN_{i} \leq \sum_{i=1}^{k} OUT_{i} \rightarrow \sum_{i=1}^{k+1} IN_{i} \leq \sum_{i=1}^{k+1} OUT_{i}$$

$$\sum_{i=1}^{k} IN_{i} \leq \sum_{i=1}^{k} OUT_{i} \rightarrow \sum_{i=1}^{k} IN_{i} + IN_{k+1} \leq \sum_{i=1}^{k} OUT_{i} + IN_{k+1} \leq \sum_{i=1}^{k} OUT_{i} + OUT_{k+1} \rightarrow \sum_{i=1}^{k+1} IN_{i}  \leq \sum_{i=1}^{k+1} OUT_{i}$$

## b) 


Ordeno el arreglo de elementos con merge sort. 

## c) 
Armo un minHeap de los primeros k elementos (O(klogk)). El resto los recorro con un ciclo y los voy comparando con el proximo del heap. Si son mayores, los swapeo y hago heapify (O(nlogk))


------------
Otra demo posible es demostrar que dados los num del input ordenados x1>=x2...>=xn cualquier subconjunto de indices tiene suma menor o igual a la propuesta por greedy. 
Asumaos que estos otros indices estan ordenados de menor a mayor. 
Luego la suma de los indices greedy - la suma de estos indices = (xg1- xo1) + (xg2 - xo2) + ... + (xgn-xon) 
se puede ver (usando x ej induccion) que oi>=gi y sabemos que los x del input estan ordenados de mayor a menor entonces xoi < xgi y xgi - xoi >0. Luego todas las diferencias son positivas y queda demostrado el teorema :)
