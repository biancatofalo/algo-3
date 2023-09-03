# Ejercicio 14
## a) 
Idea: Tomar k veces al máximo del conjunto. 

Demostracion de que el algoritmo greedy es correcto: tengo que ver que la solución es válida (es un subconjunto de S de tamaño k) y óptimo (maximiza la suma). 

Primero veo que es válido, esto es trivial, ya que el algoritmo toma k elementos de X, entonces todos los elementos de la solución greedy son elementos del conjunto X, y tengo exactamente k elementos. 

Ahora veo que es óptimo, o sea, que no hay un subconjunto de X de k elementos cuyos elementos sumados sumen más que los elementos de la solución greedy sumados.

Tengo la solución del algoritmo greedy $S_1 = \{S_{1_1}, \ldots, S_{1_k}\} \subset X$.

Supongo que existe una solución $S_2 = \{S_{2_1}, \ldots, S_{2_k}\} \subset X$ tal que $$\sum_{i=1}^{k} S_{1_i} < \sum_{i=1}^{k} S_{2_i}$$
Esto implica (ver demostración abajo) que existe $S_{2_i}$ con $1 \leq i \leq k$ tal que $S_{2_i} < S_{1_j}$ con $1 \leq j \leq k$. Sin embargo, por cómo está construida la solución greedy, no existe $S_{2_i}$ que cumpla eso, ya que $S_{2_i} \in X$, y todo elemento en $S_1$ es mayor o igual a cualquier elemento en $X$. Entonces, no existe una solución $S_2 = \{S_{2_1}, \ldots, S_{2_k}\} \subset X$ tal que $$\sum_{i=1}^{k} S_{1_i} < \sum_{i=1}^{k} S_{2_i}$$.

Demostración que falta:
$P(k) =$ $$\sum_{i=1}^{k} S_{1_i} < \sum_{i=1}^{k} S_{2_i}$$ $\rightarrow \exists  S_{2_i}$ con $1 \leq i \leq k$ tal que $S_{2_i} < S_{1_j}$ con $1 \leq j \leq k$ para todo $k \in \mathbb{N}$.

Probamos $P(k)$ con inducción en $k$:

Caso base: P(1)

Si $k=1$ es verdadero, porque $X_{1} < Y_{1} \rightarrow X_{1} < Y_{1}$.

Paso inductivo: $P(k) \rightarrow P(k+1)$
HI: $$\sum_{i=1}^{k} S_{1_i} < \sum_{i=1}^{k} S_{2_i}$$ $\rightarrow \exists S_{2_i}$ con $1 \leq i \leq k$ tal que $S_{2_i} < S_{1_j}$ con $1 \leq j \leq k$.

Queremos probar que $$\sum_{i=1}^{k+1} S_{1_i} < \sum_{i=1}^{k+1} S_{2_i}$$ $\rightarrow \exists S_{2_i}$ con $1 \leq i \leq k+1$ tal que $S_{2_i} < S_{1_j}$ con $1 \leq j \leq k+1$.

Si $$\sum_{i=1}^{k+1} S_{1_i} \geq \sum_{i=1}^{k+1} S_{2_i}$$, entonces $P(k+1)$ es trivialmente verdadero.

Si $$\sum_{i=1}^{k+1} S_{1_i} < \sum_{i=1}^{k+1} S_{2_i}$$, tenemos dos casos posibles:

1) $$\sum_{i=1}^{k} S_{1_i} < \sum_{i=1}^{k} S_{2_i}$$ $\rightarrow \exists S_{2_i}$ con $1 \leq i \leq k$ tal que $S_{2_i} < S_{1_j}$ con $1 \leq j \leq k \rightarrow \exists S_{2_i}$ con $1 \leq i \leq k+1$ tal que $S_{2_i} < S_{1_j}$ con $1 \leq j \leq k+1$.

2) $$\sum_{i=1}^{k} S_{1_i} \geq \sum_{i=1}^{k} S_{2_i}$$. Además, sabemos que $$\sum_{i=1}^{k+1} S_{1_i} < \sum_{i=1}^{k+1} S_{2_i}$$ $\rightarrow$ $$\sum_{i=1}^{k} S_{1_i} + S_{1_{k+1}} < \sum_{i=1}^{k} S_{2_i} + S_{2_{k+1}}$$. Esto solo es posible si $S_{1_{k+1}} < S_{2_{k+1}} \rightarrow \exists S_{2_i}$ con $1 \leq i \leq k+1$ tal que $S_{2_i} < S_{1_j}$ con $1 \leq j \leq k+1$.

  
