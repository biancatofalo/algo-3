### Ejercicio 3
## a)
Idea: Voy generando conjuntos de k elementos, y quedandome con el que maximiza la suma. 
Las soluciones candidatas son los subconjuntos de k elementos de {1,..,n}. 
Las soluciones válidas son las que maximizan la suma. 
Las soluciones parciales son los subconjuntos de {1,...,n} de i elementos, con $0<=i<=k$. Se extienden agregando o no el siguiente elemento. 

```cpp
#include <iostream>
#include <vector>

using namespace std;

int N;
vector<vector<int>> matriz;
int k;
int maximo;
vector<int> mejor_solucion;

//Obs: podría ir sumando a medida que agrego elementos al subconjunto (si agrego i, recorro todo el subconjunto y para cada elemento j, sumo a la suma total M[j][i]+M[i][j] y ademas sumo M[i][i]) 
int suma_conjunto(vector<int>& conjunto) {
    int res=0;
    for (int i=0; i<N; i++) {
        for (int j=0; j<N; j++) {
            res+=matriz[i][j];
        }
    }
    return res;
}

void max_suma(int k, vector<int>& sol_parcial, int valor) {
    if (k==0) {
        int suma = suma_conjunto(sol_parcial);
        if (suma > maximo) {
            maximo = suma;
            mejor_solucion = sol_parcial;
        }
        return;
    }
    //Esta rama no va a servir porque ya me quede sin elementos que mirar, y no complete los k elementos porque k!=0
    if (valor==N) {
        return;
    }
    //Hay una mejor manera de generar las soluciones parciales y es solo agregar al que tengo actualmetne los de indice mayor. Asi no se repiten subconjuntos
    sol_parcial.push_back(valor);
    max_suma(k-1, sol_parcial, valor+1);
    sol_parcial.pop_back();
    max_suma(k, sol_parcial, valor+1);
}

int main() {
    cin >> k;
    cin >> N;
    matriz.resize(N, vector<int>(N,0));
    for (int i=0; i<N; i++) {
        for (int j=0; j<N; j++) {
            int elem;
            cin >> elem;
            matriz[i][j]=elem;
        }
    }
    vector<int> sol_parcial(0);
    maximo=0;
    //le paso 0 porque voy a mirar los numeros del 0 al N-1 y los voy a ir agregando al conjunto. Empiezo por el 0.
    max_suma(k, sol_parcial, 0);
    cout << "El subconjunto que maximiza la suma es {";
    for (int i=1; i<=k;i++) {
        if (i==k) {
            cout << mejor_solucion[i-1]+1;
        } else {
            cout << mejor_solucion[i-1]+1 << ", ";
        }
        // le sumo uno porque en mejor_solucion tengo los indices, pero como I empieza a sumar en 1 hay q arreglar eso
    }
    cout << "} y su suma es " << maximo;
    return 0;
}
```

Arbol de backtracking: 
![3a](/Practica%201/images/backtracking_3a.png)
En algunos casos, corto porque k=0, y en otros porque no hay mas elementos que agregar (k=N). 
Con este algoritmo, se podan ramas que se pasan de la longitud deaseada. Otra posible poda sería si con los elementos restantes no lograra llegar a k elementos, o si sumando no logro llegar al máximo. 
Observación: la matriz era simétrica, capaz cambia algo. 

## b) 
# Complejidad temporal: 
#nodos = #subconjuntos de tamaño menor o igual a k = $$\sum_{i=0}^{k} \binom{n}{i}$$
Entonces #nodos = $O(2^n)$

Costo de cada nodo: el caso base es $O(k^2+k)$ porque copio la solución parcial, y calculo la suma rara. el costo de los nodos internos es constante. 
Complejidad = $O((k^2+k)*2^n) = O(k^{2}2^{n})$ . 
# Complejidad espacial: 
$O(k+k)=O(k)$, por el costo de tener la mejor solucion y la solucion parcial almacenadas. 

## c) 
Podriamos podar si con los elementos restantes no se pudiera llegar al máximo (aunque esto sería costoso de calcular). 

## Preguntas
a) Soluciones candidatas son conjuntos de k elementos o de cualquier cantidad de elementos? 
