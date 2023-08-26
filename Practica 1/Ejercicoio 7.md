# Ejercicio 7 
## a) 
$$
av(P, c, j) =
\begin{cases}
     indefinido & \text{si } c < 0 \lor j < c \\
     0 & \text{si } j < 0 \\
     max(av(P, j-1, c+1) + P[j], av(P, j-1, c-1) - P[j], av(P, j-1, c)) & \text{caso contrario}
\end{cases}
$$


