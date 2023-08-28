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
```cpp
#include <iostream>
#include <vector>

using namespace std;
int infinito=1e9;
//Version sin DP:
int min_costo(vector<int>& cortes, int a, int b, int i, int j) {
    if (b<a) { //revisar esta condicion
        return 0;
    }
    int minimo=infinito;

    while() {
        int costo = min_costo() + min_costo();
        if (costo<minimo) {
            minimo=costo;
        }
    }
    return j-i+minimo;
}

//Version con DP

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
    cout << "El menor costo para hacer los cortes es " << min_costo(cortes,0, cantCortes-1, 0, longitud);
    return 0;
}
```
