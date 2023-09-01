# Ejercicio 10 
## b) 

$$
f(soporte, i)_{W,S,sumaSoportes} =
\begin{cases}
     0 & \text{si } i = |P| \land soporte>=0 \\
     -\infty & \text{si } soporte < 0 \\
     max(f(S[i], i+1) + 1, f(soporte, i+1)) & \text{si } soporte = sumaSoportes \\ 
     max(f(min(soporte-W[i], S[i]), i+1) + 1, f(soporte, i+1) ) & \text{caso contrario}
\end{cases}
$$

El llamado que resuelve el problema es f(sumaSoportes, 0) 


## c) 

#include <iostream>
#include <vector>

using namespace std;

int sumaSoportes=0;
vector<int> soportes;
vector<int> pesos;
int cantCajas;
int infinito=1e9;
vector<vector<int>> memo;

int apilar_cajas(int soporte, int caja) {
    if (caja==cantCajas && soporte>=0) {
        return 0;
    }
    if (soporte<0) {
        return -infinito;
    }
    if (memo[soporte][caja]!=-1) {
        return memo[soporte][caja];
    }
    if (soporte==sumaSoportes) {
        memo[soporte][caja] = max(apilar_cajas(soportes[caja],caja+1)+1, apilar_cajas(sumaSoportes,caja+1));
    } else {
        memo[soporte][caja] = max(apilar_cajas(min(soporte-pesos[caja], soportes[caja]), caja+1)+1, apilar_cajas(soporte,caja+1));
    }
    return memo[soporte][caja];
}

int main() {
    cin >> cantCajas;
    soportes.resize(cantCajas);
    pesos.resize(cantCajas);
    for (int i=0; i<cantCajas;i++) {
        int peso;
        cin >> peso;
        int soporte;
        cin >> soporte;
        pesos[i]=peso;
        soportes[i]=soporte;
        sumaSoportes+=soporte;
    }
    memo.resize(sumaSoportes+1, vector<int>(cantCajas, -1));
    cout << "La maxima cantidad de cajas apilable es " << apilar_cajas(sumaSoportes, 0);
    return 0;
}


## Preguntas
Le puedo pasar infinito como parametro? Ya sea en la formulacion como en el codigo. 
