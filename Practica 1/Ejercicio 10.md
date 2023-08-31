# Ejercicio 10 
## b) 

$$
f(soporte, i)_{W,S} =
\begin{cases}
     0 & \text{si } i = |P| ^ soporte>=0 \\
     -\infty & \text{si } soporte < 0 \\
     max(f(S[i], i+1) + 1, f(soporte, i+1)) & \text{si } soporte = suma_soportes \\ 
     max(f(min(soporte-W[i], S[i]), i+1) + 1, f(soporte, i+1) ) & \text{caso contrario}
\end{cases}
$$

La funcion devuelve 0 si no hay cajas que poner ($i>=|P|$), $-\infnt$ si el soporte es menor a 0, o el maximo entre apilar la caja (y por lo tanto el soporte ahora es el minimo entre el soporte de la caja, y el soporte anterior menos el peso de la caja), o no apilarla. 

Empiezo con soporte=peso de todos juntos? Ahi el min(soporte-W[i], S[i]) va a dar S[i] salvo que el peso de todos los restantes sea menor al soporte de la que apilo. Si esto ocurre, en el siguiente paso va
Quisiera que soporte empieze siendo un numero muy grande tal que al agregar la primera caja, el minimo siempre de S[i]. ¿Como hago? Hago que soporte sea la suma de todos los soportes. Pero podria fallar si justo W[i] es mas grande que la suma de todos estos soportes, entonces soporte-W[i] es negativo y ahi da que el minimo es eso y 


El llamado que resuelve el problema es f()

##
