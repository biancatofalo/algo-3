# Ejercicio 4 
## a) 
Idea: generar las posibles permutaciones y ver cuál minimiza la suma. 
![4a](/Practica%201/images/backtracking_4a.png)

Cuando llega a 4 elementos, se fija si es el máximo. Pued podar si ya a suma supera al mínimo. 
Solucion candidata: cualquier permutación de {1,...,n} 
Solucion válida: minimiza la suma. 
Solución parcial: permutaciones de {1,...,i} con $1<=i<=n$. Se extienden agregando cualquier elemento de {1,...,n} que no este en la solucion aun. 

Sin podar si los que tengo hasta ahora ya superan al minimo:
```cpp
#include <iostream>
#include <vector>

using namespace std;

int N;
vector<vector<int>> matriz;
int minimo;
vector<int> perm_minimo;

int suma_rara( vector<int>& perm_parcial) {
    int suma=0;
    for (int i=0; i<perm_parcial.size()-1; i++) {
        suma += matriz[i][i+1];
    }
    suma += matriz[perm_parcial.size()-1][1];
    return suma;
}

void min_suma_rara(int k, vector<int>& perm_parcial, vector<bool>& esta) {
    if (k==0) {
        int suma = suma_rara(perm_parcial);
        if (suma < minimo || minimo==-1) {
            minimo = suma;
            perm_minimo=perm_parcial;
        }
        return;
    }
    for (int i=0; i<N; i++) {
        if (esta[i]==false) {
            perm_parcial.push_back(i);
            esta[i]=true;
            min_suma_rara(k-1, perm_parcial, esta);
            esta[i]=false;
            perm_parcial.pop_back();
        }
    }
}

int main() {
    cin >> N;
    matriz.resize(N, vector<int>(N,0));
    for (int i=0;i<N; i++) {
        for(int j=0; j<N; j++) {
            int elem;
            cin >> elem;
            matriz[i][j]=elem;
        }
    }
    minimo=-1;
    perm_minimo.resize(N);
    vector<int> perm_parcial(0);
    vector<bool> esta(N,false); //vector que en la posicion i me dice si el elemento i ya lo puse en la permutacion o no
    min_suma_rara(N, perm_parcial, esta);
    //Lo calculo todo con 0 a N-1 y luego al imprimirlo le sumo 1 para facilitar las cosas.
    cout << "El subconjunto que minimiza la suma es {";
    for (int i=0; i<N;i++) {
        if (i==N-1) {
            cout << perm_minimo[i]+1;
        } else {
            cout << perm_minimo[i]+1 << ", ";
        }
        // le sumo uno porque en mejor_solucion tengo los indices, pero como I empieza a sumar en 1 hay q arreglar eso
    }
    cout << "} y su suma es " << minimo;
    return 0;
}
```
Podando si los que tengo hasta ahora ya superan al minimo, y ademas sumando en cada paso y no al final:
```cpp
#include <iostream>
#include <vector>

using namespace std;

int N;
vector<vector<int>> matriz;
int minimo;
vector<int> perm_minimo;

void min_suma_rara(int k, vector<int>& perm_parcial, vector<bool>& esta, int s) {
    //El caso en que tengo un solo elemento en la matriz lo veo aparte
    if (N==1) {
        perm_minimo = vector<int>(1,0);
        minimo=matriz[0][0];
    }

    if (k==0) {
        int nueva_s=matriz[perm_parcial[perm_parcial.size()-1]][perm_parcial[0]];
        if (s+nueva_s < minimo || minimo==-1) {
            minimo=s+nueva_s;
            perm_minimo = perm_parcial;
        }
        return;
    }
    for (int i=0; i<N; i++) {
        if (esta[i]==false) {
            int nueva_s = (k==N) ? 0 : matriz[perm_parcial[perm_parcial.size()-1]][i];
            if (nueva_s + s < minimo || minimo==-1) {
                perm_parcial.push_back(i);
                esta[i]=true;
                min_suma_rara(k-1, perm_parcial, esta, s + nueva_s);
                esta[i]=false;
                perm_parcial.pop_back();
            }
        }
    }
}

int main() {
    cin >> N;
    matriz.resize(N, vector<int>(N,0));
    for (int i=0;i<N; i++) {
        for(int j=0; j<N; j++) {
            int elem;
            cin >> elem;
            matriz[i][j]=elem;
        }
    }
    minimo=-1;
    perm_minimo.resize(N);
    vector<int> perm_parcial(0);
    vector<bool> esta(N,false); //vector que en la posicion i me dice si el elemento i ya lo puse en la permutacion o no
    min_suma_rara(N, perm_parcial, esta, 0);
    //Lo calculo todo con 0 a N-1 y luego al imprimirlo le sumo 1 para facilitar las cosas.
    cout << "El subconjunto que minimiza la suma es {";
    for (int i=0; i<N;i++) {
        if (i==N-1) {
            cout << perm_minimo[i]+1;
        } else {
            cout << perm_minimo[i]+1 << ", ";
        }
        // le sumo uno porque en mejor_solucion tengo los indices, pero como I empieza a sumar en 1 hay q arreglar eso
    }
    cout << "} y su suma es " << minimo;
    return 0;
}
```
## b) 
### Complejidad temporal: 
#nodos = $$\sum_{i=0}^{n} i!$$
Entonces #nodos = $O(2^n)$ 
El costo de cada nodo, sumando en cada paso, es O(k+kN+N)=O(k+N+kN)=O(kN), por: copiar la perm_parcial a perm_minimo, agregar elementos atras de la parcial (kN), y el for de los nodos internos. 

### Complejidad espacial: 
$O(n^2)$ por la solucion parcial, el vector está, y perm_minimo. 

## c) 
Podar si supera al mínimo. 

# Preguntas
Complejidad temporal ?? 
