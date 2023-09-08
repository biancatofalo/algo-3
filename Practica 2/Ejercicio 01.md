$$
\text {Caso base: Si }m=0 \text{, hay 0 aristas }\rightarrow \text {hay 0 aristas que llegan a }V_i \text {, y 0 aristas que salen de } V_i \ \forall \ 1 \leq i \leq n \ \rightarrow \ d_{in}(V_i)=0 \text { y } d_{out}(V_i)=0 \ \forall \ 1 \leq i \leq n \ \rightarrow
$$

$$
\sum_{i=1}^{n} d_{in}(V_i) = \sum_{i=1}^{n} 0 = 0 \land \sum_{i=1}^{n} d_{out}(V_i) = \sum_{i=1}^{n} 0  = 0 \land |E|=0 \rightarrow \text { se cumple para } m=0
$$ 

$$
\text {Paso inductivo: Supongo que para todo digrafo D'=(V', E') con m'<m, } \sum_{i=1}^{n} d_{in_{D'}}(V´_{i}) = \sum_{i=1}^{n} d_{out_{D'}}(V´_{i}) = |E'| = m'
$$
