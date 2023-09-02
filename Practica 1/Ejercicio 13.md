# Ejercicio 13
## b) 

Idea: Recorro ambos conjuntos con indices i y j. Cuando $|P_1 [i] - P_2 [j]| \leq 1$, armo una pareja y avanzo ambos indices. 
Si $|P_1 [i] - P_2 [j]| > 1$, avanzo j porque si avanzo i se aleja mas de $P_2 [j]$. 
Si $|P_1 [i] - P_2 [j]| < -1$, avanzo i porque si avanzo j se aleja mas de $P_1 [i]$. 
Cuando alguno llega al final, corto. 
```cpp
#include <iostream>
#include <vector>

using namespace std;

int armar_parejas(vector<int>& habilidades1, vector<int>& habilidades2) {
    int cantParejas=0;
    int i=0;
    int j=0;
    while (i<habilidades1.size() && j<habilidades2.size()) {
        if (-1<= habilidades1[i]-habilidades2[j] && habilidades1[i]-habilidades2[j] <=1 ) {
            cantParejas++;
            i++;
            j++;
        } else if (-1 > habilidades1[i]-habilidades2[j]) {
             i++;
        } else {
            j++;
        }
    }
    return cantParejas;
}

int main() {
    int N;
    cin >> N;
    vector<int> habilidades1(N);
    for (int i=0; i<N; i++) {
        int habilidad;
        cin >> habilidad;
        habilidades1[i] = habilidad;
    }
    int M;
    cin >> M;
    vector<int> habilidades2(M);
    for (int i=0; i<M; i++) {
        int habilidad;
        cin >> habilidad;
        habilidades2[i] = habilidad;
    }
    cout << "La maxima cantidad de parejas posible es " << armar_parejas(habilidades1, habilidades2) << endl;
    return 0;
}
```
Complejidad: 
* Temporal: O(N+M) 
* Espacial: O(1)

## c) 
Para demostrar que el algoritmo es correcto, veo que 1) La solución es válida (todas las parejas tienen una diferencia de habilidad menor o igual a 1, no hay dos personas que esten en dos parejas, y todas las parejas tienen a una persona de cada grupo). 2) La solución es óptima 

1) 
