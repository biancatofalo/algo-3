# Ejercicio 8
## b) 

$$
min_costo({k_{0},...,k_{n-1}, i. j) =
\begin{cases}
     0 & \text{si } |c| < 0 
     {caso contrario}
\end{cases}
$$

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
