# Ejercicio 10 
## b) 

$$
f(soporte, i)_{W,S,sumaSoportes} =
\begin{cases}
     0 & \text{si } i = |P| \land soporte>=0 \\
     -\infty & \text{si } soporte < 0 \\
     max(f(S[i], i+1) + 1, f(soporte, i+1)) & \text{si } soporte = sumaSoportes \\ 
     max(f(min(soporte-W[i], S[i]), i+1) + 1, f(soporte, i+1) ) & \text{caso contrario}
\end{cases}
$$

El llamado que resuelve el problema es f(sumaSoportes, 0) 

##
