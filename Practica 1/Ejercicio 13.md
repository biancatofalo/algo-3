# Ejercicio 13
## b) 

Idea: Recorro ambos conjuntos con indices i y j. Cuando $|P_1 [i] - P_2 [j]| \leq 1$, armo una pareja y avanzo ambos indices. 
Si $|P_1 [i] - P_2 [j]| > 1$, avanzo j porque si avanzo i se aleja mas de $P_2 [j]$. 
Si $|P_1 [i] - P_2 [j]| < -1$, avanzo i porque si avanzo j se aleja mas de $P_1 [i]$. 
Cuando alguno llega al final, corto. 
```cpp

```
