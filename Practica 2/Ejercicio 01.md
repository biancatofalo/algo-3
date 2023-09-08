$$
\text {Caso base: Si }m=0 \text{, hay 0 aristas }\rightarrow \text {hay 0 aristas que llegan a }V_i \text {, y 0 aristas que salen de } V_i \ \forall \ 1 \leq i \leq n \ \rightarrow \ d_{in}(V_i)=0 \text { y } d_{out}(V_i)=0 \ \forall \ 1 \leq i \leq n \ \rightarrow
$$

$$
\sum_{i=1}^{n} d_{in}(V_i) = \sum_{i=1}^{n} 0 = 0 \land \sum_{i=1}^{n} d_{out}(V_i) = \sum_{i=1}^{n} 0  = 0 \land |E|=0 \rightarrow \text { se cumple para } m=0
$$ 

$$
\text {Paso inductivo: Supongo que para todo digrafo } D'=('V, E') \text { con m < m', } 
$$

$$
(1) \sum_{i=1}^{n} d_{in_{D'}}('V_{i}) = \sum_{i=1}^{n} d_{out_{D'}}('V_{i}) = |E'| = m' 
$$

$$
\text {Quiero ver que en D se cumple que } \sum_{i=1}^{n} d_{in_{D}}(V_{i}) = \sum_{i=1}^{n} d_{out_{D}}(V_{i}) = |E| = m
$$

$$
\text {Si tomo una arista } e=(V_{h}, V_{j}) \text { de } D \text{, y la elimino, el grafo que queda es un digrafo } D'=(V, E') \text{ con m' < m (m' = m-1) } \rightarrow \text{cumple (1)}
$$

$$
\text {Sabemos que } d_{in_{D'}} (V_{j}) = d_{in_{D}} (V_{j}) - 1 \text {, } d_{out_{D'}} (V_{h}) = d_{out_{D}} (V_{h}) - 1 \text {, } d_{in_{D'}} (V_{i}) = d_{in_{D}} (V_{i}) \ \forall \ 1 \leq i \leq n, \ j \neq i, \text{ y } d_{out_{D'}} (V_{i}) = d_{out_{D}} (V_{i}) \ \forall \ 1 \leq i \leq n, \ h \neq i. 
$$

$$
\text{ Además, } n' = n \text { porque V queda igual. Entonces }
$$

$$
\sum_{i=1}^{n} d_{in_{D}}(V_{i}) = \sum_{i=1}^{j-1} d_{in_{D'}}(V_{i}) + d_{in_{D}} (V_{j}) + \sum_{i=j+1}^{n} d_{in_{D'}}(V_{i}) = \sum_{i=1}^{j-1} d_{in_{D'}}(V_{i}) + d_{in_{D'}} (V_{j}) + 1 + \sum_{i=j+1}^{n} d_{in_{D'}}(V_{i}) = \sum_{i=1}^{n} d_{in_{D'}}(V_{i}) + 1 = m' + 1 
$$

$$
\sum_{i=1}^{n} d_{out_{D}}(V_{i}) = \sum_{i=1}^{j-1} d_{out_{D'}}(V_{i}) + d_{out_{D}} (V_{h}) + \sum_{i=j+1}^{n} d_{out_{D'}}(V_{i}) = \sum_{i=1}^{j-1} d_{out_{D'}}(V_{i}) + d_{out_{D'}} (V_{h}) + 1 + \sum_{i=j+1}^{n} d_{out_{D'}}(V_{i}) = \sum_{i=1}^{n} d_{out_{D'}}(V_{i}) + 1 = m' + 1 
$$

$$ 
\text {Entonces, } \sum_{i=1}^{n} d_{in_{D}}(V_{i}) = \sum_{i=1}^{n} d_{out_{D}}(V_{i}) = m' + 1 = m = |E|
$$
