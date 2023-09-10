Idea: tomo siempre los 3 menores, y sumo el descuento del menor. 
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int max_descuento(vector<int>& precios) {
    sort(precios.begin(), precios.end());
    int desc_max;
    int cant_acum=0;
    for (int i=0; i<precios.size(); i++) {
        if (cant_acum==0) {
            desc_max += precios[i];
        }
        cant_acum++;
        if (cant_acum==3) {
            cant_acum=0;
        }
    }
    return desc_max;
}

int main () {
    int cantCasos;
    cin >> cantCasos;
    vector<int> resultados(cantCasos);
    for (int i=0; i<cantCasos; i++) {
        int N;
        cin >> N;
        vector<int> precios(N);
        for (int j=0; j<N; j++) {
            int precio;
            cin >> precio;
            precios[j] = precio;
        }
        resultados[i] = max_descuento(precios);
    }
    for (int i=0; i<cantCasos; i++) {
        if (i==cantCasos-1) {
            cout << resultados[i];
        } else {
            cout << resultados[i] << endl;
        }
    }
    return 0;
}
```
Demostración: tomar una solucion q no tome los 3 mas caros y mostrar que si lo hiciera tendria mayor descuento. 
