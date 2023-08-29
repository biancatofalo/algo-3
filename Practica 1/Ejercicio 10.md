# Ejercicio 10 
## b) 

$$
f(soporte, i)_{W,S} =
\begin{cases}
     0 & \text{si } i = |P| \\
     -\infty & \text{si } soporte < 0 \\
     max(f(min(soporte-S[i], S[i]), i+1) + 1, f(soporte, i+1) ) & \text{caso contrario}
\end{cases}
$$

##
