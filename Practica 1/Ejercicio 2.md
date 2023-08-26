### Ejercicio 2
## a) 
${(n^2)}^{n^2}$ si no se descartan cuadrados con repetidos. 

$n^{2}!$ si se descartan cuadrados con repetidos. 

## b) 
Idea: tengo un vector de $n^2$ elementos en el que la posición i indica si el elemento i+1 ya está o no en el cuadrado. 
```cpp
#include <iostream>
#include <vector>
#include <math.h>

using namespace std;
int N;
int cantidad;
//¿Cual es la diferencia de ponerlas ahi o en el main? N y esta y cantidad

bool es_cuadrado_magico(vector<vector<int>>& cuadrado) {
    int valorPrimeraFila=0;
    for (int i=0; i<N; i++) {
        valorPrimeraFila += cuadrado[0][i];
    }
    //Sumo cada columna y veo si tiene el mismo valor que la primera fila:
    for (int j=0; j<N; j++) {
        int sumaColumna=0;
        for (int i=0; i<N; i++) {
            sumaColumna += cuadrado[i][j];
        }
        if (sumaColumna!=valorPrimeraFila) {
            return false;
        }
    }
    //Sumo cada fila y veo si tiene el mismo valor que la primera fila:
    for (int i=0; i<N; i++) {
        int sumaFila=0;
        for (int j=0; j<N; j++) {
            sumaFila += cuadrado[i][j];
        }
        if (sumaFila!=valorPrimeraFila) {
            return false;
        }
    }
    //Sumo cada diagonal y veo si tiene el mismo valor que la primera fila:
    int sumaDiagonal1=0;
    for (int i=0; i<N; i++) {
        sumaDiagonal1 += cuadrado[i][i];
    }
    if (sumaDiagonal1!=valorPrimeraFila) {
        return false;
    }

    int sumaDiagonal2=0;
    for (int i=0; i<N; i++) {
        sumaDiagonal2 += cuadrado[i][cuadrado.size()-1-i];
    }
    if (sumaDiagonal2!=valorPrimeraFila) {
        return false;
    }
    return true;
}

void contar_cuadrados(int j, int i, int N, vector<int>& esta, vector<vector<int>>& cuadrado_parcial) {
    if (i==N && es_cuadrado_magico(cuadrado_parcial)) {
        cantidad++;
        return;
    }
    int sig_j = j==N-1 ? 0 : j+1;
    int sig_i = (sig_j==0) ? i+1 : i;
    for (int h=0; h<esta.size(); h++) {
        if (esta[h]==0) {
            cuadrado_parcial[i][j] = h+1;
            esta[h]=1;
            contar_cuadrados(sig_j, sig_i, N, esta, cuadrado_parcial);
            esta[h]=0;
            cuadrado_parcial[i][j] = -1;
        }
    }
}

int main() {
    cin >> N;
    vector<int> esta(pow(N,2),0);
    vector<vector<int>> cuadrado_parcial(N,vector<int>(N,-1));
    cantidad=0;
    contar_cuadrados(0,0,N,esta, cuadrado_parcial);
    cout << "La cantidad de cuadrados magicos de orden " << N << " es: " << cantidad;
    return 0;
}
```
Arbol de backtracking: 

![imagen2b](/Practica%201/images/backtracking_2b.png) 

Complejidad: 
#nodos = $n^2!$
costo de cada nodo = $n^2$ de chequear si es mágico, y $n^2$ si no es el caso base. 

Entonces la complejidad temporal es $O((n^2)!n^2)$

## c) 
Intuitivamente, la primera posición tiene $n^2$ opciones, la segunda $n^2-1$, ..., la n-esima 1 opcion $\rightarrow O(n^2(n^2-1)...1)=O((n^2)!)$

## d) 
Idea: Tengo un parámetro que es un vector N, el cual indica en la posición i la suma de la fila i, y otro que indica en la posición j la suma de la columna j. 
```cpp
#include <iostream>
#include <vector>
#include <math.h>

using namespace std;
int N;
int cantidad;
vector<int> sumaFila;
vector<int> sumaColumna;

bool es_cuadrado_magico(vector<vector<int>>& cuadrado) {
    int valorPrimeraFila=0;
    for (int i=0; i<N; i++) {
        valorPrimeraFila += cuadrado[0][i];
    }

    //Obs: tengo que chequear la columna y fila igual, porque en contar_cuadrados solo descarto las opciones en que me paso del
    //numero magico, pero no las que me quedo corta.
    //Sumo cada columna y veo si tiene el mismo valor que la primera fila:
    for (int j=0; j<N; j++) {
        int sumaColumna=0;
        for (int i=0; i<N; i++) {
            sumaColumna += cuadrado[i][j];
        }
        if (sumaColumna!=valorPrimeraFila) {
            return false;
        }
    }
    //Sumo cada fila y veo si tiene el mismo valor que la primera fila:
    for (int i=0; i<N; i++) {
        int sumaFila=0;
        for (int j=0; j<N; j++) {
            sumaFila += cuadrado[i][j];
        }
        if (sumaFila!=valorPrimeraFila) {
            return false;
        }
    }

    //Sumo cada diagonal y veo si tiene el mismo valor que la primera fila:
    int sumaDiagonal1=0;
    for (int i=0; i<N; i++) {
        sumaDiagonal1 += cuadrado[i][i];
    }
    if (sumaDiagonal1!=valorPrimeraFila) {
        return false;
    }

    int sumaDiagonal2=0;
    for (int i=0; i<N; i++) {
        sumaDiagonal2 += cuadrado[i][cuadrado.size()-1-i];
    }
    if (sumaDiagonal2!=valorPrimeraFila) {
        return false;
    }
    return true;
}

void contar_cuadrados(int j, int i, int N, vector<int>& esta, vector<vector<int>>& cuadrado_parcial) {
    if (i==N) {
        if (es_cuadrado_magico(cuadrado_parcial)) {
            cantidad++;
        }
        return;
    }
    int sig_j = j==N-1 ? 0 : j+1;
    int sig_i = (sig_j==0) ? i+1 : i;
    for (int h=0; h<esta.size(); h++) {
        if (esta[h]==0 && ((sumaFila[i]+h+1)<=(N*N*N + N)/2) && ((sumaColumna[j]+h+1)<=(N*N*N + N)/2)) {
                cuadrado_parcial[i][j] = h+1;
                esta[h]=1;
                sumaFila[i] += h;
                sumaColumna[j] += h;
                contar_cuadrados(sig_j, sig_i, N, esta, cuadrado_parcial);
                esta[h]=0;
                cuadrado_parcial[i][j] = -1;
                sumaFila[i] -= h;
                sumaColumna[j] -= h;
        }
    }
}

int main() {
    cin >> N;
    vector<int> esta(pow(N,2),0);
    vector<vector<int>> cuadrado_parcial(N,vector<int>(N,-1));
    sumaColumna.resize(N,0);
    sumaFila.resize(N,0);
    cantidad=0;
    contar_cuadrados(0,0,N,esta, cuadrado_parcial);
    cout << "La cantidad de cuadrados magicos de orden " << N << " es: " << cantidad;
    return 0;
}
```
Esta poda se podría mejorar si tambien se chequea que las diagonales no superen el número mágico. Además, cada vez que termina una fila podría compararla con el valor de la primera fila (y si ya no son iguales, descartar esa rama porque alguna (o ambas) no suman el número mágico)). 

## e) 
$n^2(n^2+1)/2 = nM \leftrightarrow M = n^2(n^2+1)/2n = (n^4+n^2)/2n = (n^3+n)/2$
```cpp
#include <iostream>
#include <vector>
#include <math.h>

using namespace std;
int N;
int cantidad;
vector<int> sumaFila;
vector<int> sumaColumna;

bool es_cuadrado_magico(vector<vector<int>>& cuadrado) {
    int valorPrimeraFila=0;
    for (int i=0; i<N; i++) {
        valorPrimeraFila += cuadrado[0][i];
    }

    //Obs: tengo que chequear la columna y fila igual, porque en contar_cuadrados solo descarto las opciones en que me paso del
    //numero magico, pero no las que me quedo corta.
    //Sumo cada columna y veo si tiene el mismo valor que la primera fila:
    for (int j=0; j<N; j++) {
        int sumaColumna=0;
        for (int i=0; i<N; i++) {
            sumaColumna += cuadrado[i][j];
        }
        if (sumaColumna!=valorPrimeraFila) {
            return false;
        }
    }
    //Sumo cada fila y veo si tiene el mismo valor que la primera fila:
    for (int i=0; i<N; i++) {
        int sumaFila=0;
        for (int j=0; j<N; j++) {
            sumaFila += cuadrado[i][j];
        }
        if (sumaFila!=valorPrimeraFila) {
            return false;
        }
    }

    //Sumo cada diagonal y veo si tiene el mismo valor que la primera fila:
    int sumaDiagonal1=0;
    for (int i=0; i<N; i++) {
        sumaDiagonal1 += cuadrado[i][i];
    }
    if (sumaDiagonal1!=valorPrimeraFila) {
        return false;
    }

    int sumaDiagonal2=0;
    for (int i=0; i<N; i++) {
        sumaDiagonal2 += cuadrado[i][cuadrado.size()-1-i];
    }
    if (sumaDiagonal2!=valorPrimeraFila) {
        return false;
    }
    return true;
}

void contar_cuadrados(int j, int i, int N, vector<int>& esta, vector<vector<int>>& cuadrado_parcial) {
    if (i == N) {
        if (es_cuadrado_magico(cuadrado_parcial)) {
            cantidad++;
        }
        return;
    }
    int sig_j = j == N - 1 ? 0 : j + 1;
    int sig_i = (sig_j == 0) ? i + 1 : i;
    for (int h = 0; h < esta.size(); h++) {
        if (esta[h] == 0 && ((sumaFila[i] + h + 1) <= ((N * N * N + N) / 2)) &&
            ((sumaColumna[j] + h + 1) <= (N * N * N + N) / 2)) {
            if (j == N - 1 && sumaFila[i] + h + 1 != ((N * N * N + N) / 2)) {
                //si con ese h la fila no suma el numero magico, la descarto.
            } else if (i == N - 1 && sumaColumna[j] + h + 1 != (N * N * N + N) / 2) {
                //si estoy en la ultima fila, antes de completar cada columna chequeo si suma el numero magico.
            } else {
                cuadrado_parcial[i][j] = h + 1;
                esta[h] = 1;
                sumaFila[i] += (h + 1);
                sumaColumna[j] += (h + 1);
                contar_cuadrados(sig_j, sig_i, N, esta, cuadrado_parcial);
                esta[h] = 0;
                cuadrado_parcial[i][j] = -1;
                sumaFila[i] -= (h + 1);
                sumaColumna[j] -= (h + 1);
            }
        }
    }
}

int main() {
    cin >> N;
    vector<int> esta(pow(N,2),0);
    vector<vector<int>> cuadrado_parcial(N,vector<int>(N,-1));
    sumaColumna.resize(N,0);
    sumaFila.resize(N,0);
    cantidad=0;
    contar_cuadrados(0,0,N,esta, cuadrado_parcial);
    cout << "La cantidad de cuadrados magicos de orden " << N << " es: " << cantidad;
    return 0;
}
```
Esto se podría aprovechar verificando cada vez que completo una fila/columna si suma el número mágico. 

## Preguntas 
En casos como este, se puede podar por optimalidad? Si, debería ser algo como ya se que por este camino no supero al actual. 
El arbol de backtracking incluye los casos que voy descartando? 
c) Formalmente
La complejidad es #nodos o #hojas * costo de casos base o nodo interno? 

