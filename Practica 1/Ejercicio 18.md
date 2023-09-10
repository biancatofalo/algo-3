# Ejercicio 18

## a)

Tengo mi solución greedy $G = {G_1,...,G_n}$, que es una permutación de $X$, y una solución $Y = {Y_1,...,Y_n}$, que también es una permutación de $X$. 
Quiero ver que si $h \leq n$ $$\sum_{i=1}^{h} mex({{G_1,...,G_i}}) \geq \sum_{i=1}^{h} mex({{Y_1,...,Y_i}})$$
Por inducción en h: 
$P(j) =$ $$\sum_{i=1}^{j} mex({{G_1,...,G_i}}) \geq \sum_{i=1}^{j} mex({{Y_1,...,Y_i}})$$

Caso base: $j=0$. 
Trivial, $0 \leq 0$. 

Paso inductivo: 
$$\sum_{i=1}^{k} mex({{G_1,...,G_i}}) \geq \sum_{i=1}^{k} mex({{Y_1,...,Y_i}}) \rightarrow \sum_{i=1}^{k+1} mex({{G_1,...,G_i}}) \geq \sum_{i=1}^{k+1} mex({{Y_1,...,Y_i}})$$

$$\sum_{i=1}^{k+1} mex({{G_1,...,G_i}}) = (\sum_{i=1}^{k} mex({{G_1,...,G_i}})) + mex({{G_1,...,G_{k+1}}}) \geq_{HI} (\sum_{i=1}^{k} mex({{Y_1,...,Y_i}})) + mex({{G_1,...,G_{k+1}}}) \geq_{Demo2} (\sum_{i=1}^{k} mex({{Y_1,...,Y_i}})) + mex({{Y_1,...,Y_{k+1}}}) = \sum_{i=1}^{k+1} mex({{Y_1,...,Y_i}}) $$

Demo2: 
Quiero ver que $m = mex({{G_1,...,G_{k+1}}}) \geq mex({{Y_1,...,Y_{k+1}}})$ 

Tengo 2 casos: 
* $m = k+1$:
Ademas sabemos que $mex({{Y_1,...,Y_{k+1}}}) \leq k+1$. Listo, queda probado.
* $m < k+1$:
Como ${G_1,...,G_{k+1}}$ es un subconjunto de $X$, sabemos que $0...m-1 \in X$, y $m \notin X$ (ya que si m no está en los primeros k elementos, siendo menor o igua a k, no va a estar en los siguientes, ya que están en orden).
Además, como $Y$ es una permutación de $X$, $m \notin Y \rightarrow m \notin {Y_1,...,Y_{k+1}} \rightarrow mex({{Y_1,...,Y_{k+1}}}) \leq m$

## b) 
Crear un arreglo de n posiciones. El mex está entre 0 y n, entonces vas recorriendo y tachando los que están en el conjunto en O(n). Luego en O(n) recorres lo que no tachaste y te quedas con el minimo. 
