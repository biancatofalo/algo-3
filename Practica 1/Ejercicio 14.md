# Ejercicio 14
## a) 
Idea: Tomar k veces al máximo del conjunto. 

Demostracion de que el algoritmo greedy es correcto: tengo que ver que la solución es válida (es un subconjunto de S de tamaño k) y óptimo (maximiza la suma). 

Primero veo que es válido: esto es trivial, ya que el algoritmo toma k elementos de X, entonces todos los elementos de la solución greedy son elementos del conjunto X, y tengo exactamente k elementos. 

Ahora veo que es óptimo, o sea, que no hay un subconjunto de X de k elementos cuyos elementos sumados sumen mas que los elementos de la solución greedy sumados. 

Tengo la solución del algoritmo greedy S_{1} 

