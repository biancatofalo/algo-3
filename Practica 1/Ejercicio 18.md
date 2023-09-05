Tengo mi solución greedy $G = {G_1,...,G_n}$, que es una permutación de $X$, y una solución $Y = {Y_1,...,Y_n}$, que también es una permutación de $X$. 
Quiero ver que si $h \leq n$ $$\sum_{i=1}^{h} mex({{G_1,...,G_i}}) \geq \sum_{i=1}^{h} mex({{Y_1,...,Y_i}})$$
Por inducción en h: 
$\text {P(j) = }$ $$\sum_{i=1}^{j} mex({{G_1,...,G_i}}) \geq \sum_{i=1}^{j} mex({{Y_1,...,Y_i}})$$

Caso base: $j=0$. 
Trivial, $0 \leq 0$. 

Paso inductivo: 
$$\sum_{i=1}^{j} mex({{G_1,...,G_i}}) \geq \sum_{i=1}^{j} mex({{Y_1,...,Y_i}}) \rightarrow \sum_{i=1}^{j+1} mex({{G_1,...,G_i}}) \geq \sum_{i=1}^{j+1} mex({{Y_1,...,Y_i}})$$
