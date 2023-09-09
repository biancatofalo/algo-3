# Ejercicio 7 
## b) 
$$
av(P, c, j) =
\begin{cases}
     indefinido & \text{si } c < 0 \lor j < c \\
     0 & \text{si } j < 0 \\
     max(av(P, c+1, j-1) + P[j], av(P, c-1, j-1) - P[j], av(P, c, j-1)) & \text{caso contrario}
\end{cases}
$$

## c) 
El dato que es respuesta al problema es av(P, 0, |P|-1) (quiero ver cual es la maxima ganancia, si al finalizar el ultimo día tengo 0 asteroides). (Obs: el dia 1 es j=0, y el ultimo dia es j=|P|-1)). 

## d) 
```cpp
#include <iostream>
#include <vector>

using namespace std;
//Dejo a P como parametro fijo para no modificarlo en cada paso y no generar mas estados.
vector<vector<int>> memo;
int infinito=1e9;

int maximo(int a, int b, int c) {
    return max(a,max(b,c));
}

// i=asteroides final del dia j; j=dia.
int max_ganancia(vector<int>& precios, int i, int j) {
    if (i<0 || (j+1<i && i>0)) {
        return -infinito;
    }
    if (j<0) {
        return 0;
    }
    if (memo[i][j] != -2) {
        return memo[i][j];
    }
    memo[i][j]=maximo(max_ganancia(precios,i+1,j-1)+precios[j], max_ganancia(precios,i-1,j-1)-precios[j], max_ganancia(precios,i,j-1));
    return memo[i][j];
}

int main() {
    int dias;
    cin >> dias;
    vector<int> precios(dias);
    for(int i=0; i<dias; i++) {
        int elem;
        cin >> elem;
        precios[i]=elem;
    }
    memo.resize(dias, vector<int>(dias, -2));
    cout << "La maxima ganancia es " << max_ganancia(precios, 0, precios.size()-1);
    return 0;
}
```
El parámetro i va desde 0 a la cantidad de días (|P|) como mucho. El parámetro j va del ultimo (j=|P|-1) al primer día (j=0) (cuando j<0, no mira memo, sino que es el caso base). 

## e) 
```cpp
#include <iostream>
#include <vector>

using namespace std;
//Dejo a P como parametro fijo para no modificarlo en cada paso y no generar mas estados.
vector<vector<int>> memo;
int infinito=1e9;

int maximo(int a, int b, int c) {
    return max(a,max(b,c));
}

// i=asteroides final del dia j; j=dia.
int max_ganancia(vector<int>& precios, int a, int b, int dias) {
    int j=0;
    while (j < dias) {
        int i = 0;
        while (i < dias) {
            //Casos base
            if (j + 1 < i) {
                memo[i][j] = -infinito;
            } else if (j == 0) {
                //cuando j=0 solo no va haber entrado en el primer caso si i=0 o si i=1
                if (i == 0) {
                    memo[i][j] = 0;
                } else if (i == 1) {
                    memo[i][j] = -precios[j];
                }
            // No casos base: 
            } else {
                if (i==0) {
                    memo[i][j] = max(memo[i][j-1], memo[i+1][j-1]+precios[j]);
                } else if (i==dias-1){
                    memo[i][j] = max(memo[i][j-1], memo[i-1][j-1]+precios[j]);
                } else {
                    memo[i][j] = max(memo[i][j-1], max(memo[i+1][j-1]+precios[j], memo[i-1][j-1]-precios[j]));
                }
            }
            i++;
        }
        j++;
    }
    return memo[a][b];
}

int main() {
    int dias;
    cin >> dias;
    vector<int> precios(dias);
    for(int i=0; i<dias; i++) {
        int elem;
        cin >> elem;
        precios[i]=elem;
    }
    memo.resize(dias, vector<int>(dias, -2));
    cout << "La maxima ganancia es " << max_ganancia(precios, 0, precios.size()-1, dias);
    return 0;
}
```

# Preguntas: 
Esta bien poner tantos ifs en la version bottom-up? los tuve q poner porque habian muchos casos en que la matriz se me iba de rango >:( 
