# Ejercicio 1 
## a) 
(0,0,0), (0,0,1), (0,1,0), (0,1,1), (1,0,0), (1,0,1), (1,1,0), (1,1,1). 

## b) 
(0,1,0), (1,0,1). 

## c) 
(0), (1), (0,0), (0,1), (1,0), (1,1), (0,0,0), (0,0,1), (0,1,0), (0,1,1), (1,0,0), (1,0,1), (1,1,0), (1,1,1). 

## d) 
![imagen1](/Practica%201/images/backtracking_d.png) 

## e) 
La idea es devolver V si hay un subconjunto de C que sume k. Entonces, la función ve si hay alguna sin el último que sume k, o si hay alguno con el último que sume k (viendo si hay alguno sin el último que sume k-último). 

## f) 
#nodos = $$\sum_{i=0}^{n} 2^{i}\$$
Costo de cada nodo: constante.  
Complejidad = O(2^{n})

## g) 
![imagen2](/Practica%201/images/backtracking_1g.png) 

## h) 
* La suma de los restantes no llega a k (podar pos factibilidad). 
* Si j=0, da true y corto (porque ya encontré solución).

  ## j)
  Idea: tener una variable global S a la que se e van agregando y quitando elementos. Esto último es importante para que al volver de los llamados recursivos, los elementos no esten.
```cpp
#include <iostream>
#include <vector>

using namespace std;

//Ejercicio 1:
//Para todos:
int aSumar, cant;
vector<int> C;
//Para con solucion:
bool existe;
vector<int> solucion(0);
//Tengo una variable global con la solución.

bool subset_sumSinPodas (vector<int> C, int i, int j) {
    if (i==-1) {
        return j==0;
    } else {
        return subset_sumSinPodas(C,i-1,j) || subset_sumSinPodas(C,i-1,j-C[i-1]);
    }
}

bool subset_sumConPodas(vector<int> C, int i, int j) {
    if (j<0) {
        return false;
    }
    if (i==-1) {
        return j==0;
    } else {
        return subset_sumConPodas(C,i-1,j) || subset_sumConPodas(C,i-1,j-C[i-1]);
    }
}

void subset_sumConSolucion(vector<int> C, int i, int j, vector<int>& sol_parcial) {
    if (j==0) {
        solucion = sol_parcial;
        existe = true;
        return;
    }
    if (j<0) {
        return;
    }
    if (i==-1) {
        return;
    }
    subset_sumConSolucion(C,i-1,j, sol_parcial);
    sol_parcial.push_back(C[i]);
    subset_sumConSolucion(C,i-1,j-C[i], sol_parcial);
    sol_parcial.pop_back();
}

/*
Main para sin solucion:
int main() {
    cin >> aSumar;
    cin >> cant;
    C.resize(cant);
    for (int i=0; i<cant; i++) {
        int elem;
        cin >> elem;
        C[i]=elem;
    }
    cout << (subset_sumConPodas(C,C.size(), aSumar)==true ? "Existe" : "No existe");
    return 0;
}
 */
//Main para con solucion:
//OBS: es mas prolijo solo llamar a la funcion desde el main, y que en esta se cree el vector sol_parcial, la variable existe, etc., y llame a la funcion que hice mas arriba. 
int main() {
    cin >> aSumar;
    cin >> cant;
    C.resize(cant);
    for (int i=0; i<cant; i++) {
        int elem;
        cin >> elem;
        C[i]=elem;
    }
    existe = false;
    vector<int> sol_parcial(0);
    subset_sumConSolucion(C, C.size()-1, aSumar, sol_parcial);
    cout << (existe ? "Existe" : "No existe") << endl;
    if (existe) {
        cout << "El subconjunto que suma lo solicitado es {";
        for(int j=0; j<solucion.size(); j++) {
            if (j!=solucion.size()-1) {
                cout << solucion[j] << ", ";
            } else {
                cout << solucion[j];
            }
        }
        cout << "}" << endl;
    }
    return 0;
}
```
### Preguntas
# g) 
La diferencia entre arbol de recursion y de backtracking es...? 
