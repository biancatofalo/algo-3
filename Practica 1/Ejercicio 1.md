# Ejercicio 1 
## a) 
Todos los posibles subconjutnos son (0,0,0), (0,0,1), (0,1,0), (0,1,1), (1,0,0), (1,0,1), (1,1,0), (1,1,1). 

## b) 
(0,1,0), (1,0,1). 

## c) 
(0), (1), (0,0), (0,1), (1,0), (1,1), (0,0,0), (0,0,1), (0,1,0), (0,1,1), (1,0,0), (1,0,1), (1,1,0), (1,1,1). 

## d) 
![imagen1](/Practica 1/images/backtracking_d.png) 
no puedo poner la imagen xd

## e) 
La idea es devolver V si hay un subconjunto de C que sume k. Entonces, la función ve si hay alguna sin el último que sume k, o si hay alguno con el último que sume k (viendo si hay alguno sin el último que sume k-último). 

## f) 
#nodos= $\sum_{i=0}^{n} 2^{i}\$
Costo de cada nodo: constante
Complejidad=O(n)

## g) 

