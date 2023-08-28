# Ejercicio 8
## b) 
$$
minCosto({k_{0},...,k_{n-1}}, i, j) =
\begin{cases}
     0 & \text{si } c < 0 \\
     j - i + \min_{k_i \in C \atop 0 \leq i < n} \left( minCosto({k_{0},...,k_{i-1}}, i, k_{i}) + minCosto({k_{i+1},...,k_{n-1}}, k_{i}, j) \right) & \text{caso contrario}
\end{cases}
$$

Los parametros son (cortes, 0, longitud) 

## c) 
Version top-down: está mal, lo hice considerando que C estaba ordenado.  
```cpp
#include <iostream>
#include <vector>

using namespace std;
int infinito=1e9;
/*
//Version sin DP:
int min_costo(vector<int>& cortes, int a, int b, int i, int j) {
    if (b<a) { //revisar esta condicion
        return 0;
    }
    int minimo=infinito;
    int k0=a;
    while(k0!=b+1) {
        int costo = min_costo(cortes, a, k0-1, i, cortes[k0]) + min_costo(cortes, k0+1,b,cortes[k0],j);
        if (costo<minimo) {
            minimo=costo;
        }
        k0++;
    }
    return j-i+minimo;
}
*/

//Version con DP:
vector<vector<vector<vector<int>>>> memo;

int min_costo_DP(vector<int>& cortes, int a, int b, int i, int j) {
    if (b<a) {
        return 0;
    }
    if (memo[a][b][i][j]!=-1) {
        return memo[a][b][i][j];
    }
    int minimo=infinito;
    int k0=a;
    while(k0!=b+1) {
        int costo = min_costo_DP(cortes, a, k0-1, i, cortes[k0]) + min_costo_DP(cortes, k0+1,b,cortes[k0],j);
        if (costo<minimo) {
            minimo=costo;
        }
        k0++;
    }
    memo[a][b][i][j] = j-i+minimo;
    return memo[a][b][i][j];
}

int main() {
    int cantCortes;
    cin >> cantCortes;
    vector<int> cortes(cantCortes);
    for (int i=0; i<cantCortes; i++) {
        int elem;
        cin >> elem;
        cortes[i]=elem;
    }
    int longitud;
    cin >> longitud;
    memo.resize(cantCortes, vector<vector<vector<int>>>(cantCortes, vector<vector<int>>(longitud+1,vector<int>(longitud+1, -1))));
    cout << "El menor costo para hacer los cortes es " << min_costo_DP(cortes,0, cantCortes-1, 0, longitud);
    return 0;
}
```

## Preguntas
Cual seria el tamaño de la matriz? 
Esta bien esto?: 
a va de 0 a cantCortes-1, b tambien i va de 0 a l y j tambien, pero los casos en que a<b no los uso ?? armo la matriz asi igual? Lo mismo con i y j, i siempre es menor que j. 
