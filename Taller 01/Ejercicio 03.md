(Falta revisar el tema de la salida porque deja un endl de mas al final)
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;


void imprimir_cadenas (int N, int H, int distActual, int indice, vector<int>& sol_parcial) {
    if (indice == N) {
        if (distActual==H) {
            for (int i=0; i<sol_parcial.size(); i++) {
                if (i==sol_parcial.size()-1) {
                    cout << sol_parcial[i] << endl;
                } else {
                    cout << sol_parcial[i];
                }
            }
        }
    } else if (distActual==H) { // poda 1: si ya llegue a la distancia, solo agrego 0's.
        sol_parcial.push_back(0);
        imprimir_cadenas(N,H,distActual, indice+1, sol_parcial);
        sol_parcial.pop_back();
    } else {
        sol_parcial.push_back(0);
        imprimir_cadenas(N,H,distActual, indice+1, sol_parcial);
        sol_parcial.pop_back();
        sol_parcial.push_back(1);
        imprimir_cadenas(N,H,distActual+1, indice+1, sol_parcial);
        sol_parcial.pop_back();
    }
}

int main () {
    int cantCasos;
    cin >> cantCasos;
    vector<pair<int, int>> datos(cantCasos);
    for (int i=0; i<cantCasos; i++) {
        int N;
        int H;
        cin >> N;
        cin >> H;
        datos[i] = make_pair(N,H);
    }
    for (int i=0; i<cantCasos; i++) {
        if (i==cantCasos-1) {
            vector<int> sol_parcial(0);
            imprimir_cadenas(datos[i].first, datos[i].second, 0, 0, sol_parcial);
        } else {
            vector<int> sol_parcial(0);
            imprimir_cadenas(datos[i].first, datos[i].second, 0, 0, sol_parcial);
            cout << endl;
        }
    }
    return 0;
}
```
