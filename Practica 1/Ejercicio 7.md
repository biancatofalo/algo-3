# Ejercicio 7 
## b) 
$$
av(P, c, j) =
\begin{cases}
     indefinido & \text{si } c < 0 \lor j < c \\
     0 & \text{si } j < 0 \\
     max(av(P, j-1, c+1) + P[j], av(P, j-1, c-1) - P[j], av(P, j-1, c)) & \text{caso contrario}
\end{cases}
$$

## c) 
El dato que es respuesta al problema es av(P, 0, |P|-1) (quiero ver cual es la maxima ganancia, si al finalizar el ultimo día tengo 0 asteroides). (Obs: el dia 1 es j=0, y el ultimo dia es j=|P|-1)). 

## d) 
