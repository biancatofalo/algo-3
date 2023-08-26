# Ejercicio 1 
## a) 
Todos los posibles subconjutnos son (0,0,0), (0,0,1), (0,1,0), (0,1,1), (1,0,0), (1,0,1), (1,1,0), (1,1,1). 

## b) 
(0,1,0), (1,0,1). 

## c) 
(0), (1), (0,0), (0,1), (1,0), (1,1), (0,0,0), (0,0,1), (0,1,0), (0,1,1), (1,0,0), (1,0,1), (1,1,0), (1,1,1). 

## d) 
![imagen1](/images/backtracking_d.png)

## e) 
La idea es devolver V si hay un subconjunto de C que sume k. Entonces, la función ve si hay alguna sin el último que sume k, o si hay alguno con el último que sume k (viendo si hay alguno sin el último que sume k-último). 

## f) 
#nodos= $/sum$
