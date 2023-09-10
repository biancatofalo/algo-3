$$
\text {Si suponemos que todos los grados son distintos, y ordenamos los grados de } {V_1, V_2, ..., V_n} \ , \ d(V_1) < d(V_2) < ... < d(V_n)
$$

$$
\text {Sabemos que } V_1 \geq 0 \text {. Con esto, podemos ver que } 
d(V_i) \geq i-1 \ \forall \ 1 \leq i \leq n 
$$

$$
\text {Por otro lado, el máximo grado que puede tener } V_n \text{es n-1 (está conectado a todos los nodos). Veamos dos casos: } 
$$

$$
a) \ d(V_n) < n-1 \rightarrow d(V_i) \leq i-2 \rightarrow d(V_1) \leq -1 \text {. Esto es absurdo, entonces no es posible que } d(V_n) \leq n-2
$$

$$
b) \ d(V_n) = n-1 \rightarrow d(V_i) \leq i-1 \rightarrow d(V_1) < 0 \text {Ademas sabiamos que } d(V_i) \geq i-1 \rightarrow d(V_i)=i-1 \rightarrow d(V_1)=0 \text{. Esto es absurdo, porque } V_n \text { se conecta a todos los nodos. Entonces no es posible que } d(V_n) = n-1 .
$$

$$
\text {Así, ambos casos nos llevan a absurdos } \rightarrow \text {No es verdad que todos los grados son distintos}
$$

