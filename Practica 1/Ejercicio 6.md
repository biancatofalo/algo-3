### Ejercicio 6
## a) 
$$
cc(B,c) = 
\begin{cases}
    (\infty, \infty) \\ \\ \\ \\ \\ \\ \\ \\ \\  \text{si } i=|B| \land j>0\\
    (0,0) \\ \\ \\ \\ \\ \\ \\ \\ \\ \\ \\ \\ \\  \text{si } j\leq 0\\
    min(min(cc({b2,...,bn}, c-b1).first+b1, cc({b2,...,bn}, c-b1).second+1), (cc({b2,...,bn}, c-b1).first, cc({b2,...,bn}, c-b1).second))) \text{caso contrario}
\end{cases}
$$

## b) 
```cpp
#include <iostream>
#include <vector>

using namespace std;

int costo;
int infinito=1e9;
vector<int> b(0);

//i=indice que veo; j=precio restante
pair<int,int> traga_monedas (vector<int>&b, int i, int j) {
    if (i<0 && j>0) {
        return make_pair(infinito, infinito);
    }
    if (j<=0) {
        return make_pair(0,0);
    }
    int iesimo=b[i];
    b.pop_back();
    pair<int,int> con_billete_i = traga_monedas(b, i-1, j-iesimo);
    pair<int,int> sin_billete_i = traga_monedas(b, i-1, j);
    b.push_back(iesimo);

    int sumaBillettes;
    int cantBilletes;
    if (con_billete_i.first+b[i] == sin_billete_i.first) {
        if (con_billete_i.second < sin_billete_i.second) {
            return make_pair(con_billete_i.first+b[i], con_billete_i.second+1);
        }
        return make_pair(sin_billete_i.first, sin_billete_i.second);
    }
    if (con_billete_i.first+b[i] < sin_billete_i.first) {
        return make_pair(con_billete_i.first+b[i], con_billete_i.second+1);
    }
    return make_pair(sin_billete_i.first, sin_billete_i.second);
}

int main() {
    int cant;
    cin >> cant;
    vector<int> billetes(0);
    for (int i=0; i<cant; i++) {
        int elem;
        cin >> elem;
        billetes.push_back(elem);
    }
    int costo;
    cin >> costo;
    pair<int, int> res = traga_monedas(billetes, billetes.size()-1, costo);
    cout << res.first << ", " << res.second;
    return 0;
}
```
La complejidad temporal de este algoritmo es la cantidad de nodos posibles * costo de cada nodo = $2^{n} * O(n)$ = $O(2^{n}*n)$. El costo de cada nodo es O(n) por el push_bak(iesimo) (que se podría evitar facilmente ya que no hace falta quitar y agregar elementos porque tenemos el indice i pero creo que el ejercicio apuntaba a eso ya que en el c) aclara explicitamente que no modifiquemos b). 
La idea de hacerlo primero asi es ver que en vez de hacer esto podrias hacer lo del c), que es tener parametros numericos que representan un estado del problema, y poder memorizar con eso. 

## c) 
```cpp
#include <iostream>
#include <vector>

using namespace std;

int costo;
int infinito=1e9;
vector<int> b(0);

//i=indice que veo; j=precio restante
pair<int,int> traga_monedas (int i, int j) {
    if (i<0 && j>0) {
        return make_pair(infinito, infinito);
    }
    if (j<=0) {
        return make_pair(0,0);
    }
    pair<int,int> con_billete_i = traga_monedas(i-1, j-b[i]);
    pair<int,int> sin_billete_i = traga_monedas(i-1, j);

    int sumaBillettes;
    int cantBilletes;
    if (con_billete_i.first+b[i] == sin_billete_i.first) {
        if (con_billete_i.second < sin_billete_i.second) {
            return make_pair(con_billete_i.first+b[i], con_billete_i.second+1);
        }
        return make_pair(sin_billete_i.first, sin_billete_i.second);
    }
    if (con_billete_i.first+b[i] < sin_billete_i.first) {
        return make_pair(con_billete_i.first+b[i], con_billete_i.second+1);
    }
    return make_pair(sin_billete_i.first, sin_billete_i.second);
}


int main() {
    int cant;
    cin >> cant;
    for (int i=0; i<cant; i++) {
        int elem;
        cin >> elem;
        b.push_back(elem);
    }
    int costo;
    cin >> costo;
    pair<int, int> res = traga_monedas(b.size()-1, costo);
    cout << res.first << ", " << res.second;
    return 0;
}
```
cc'_B_ tiene superposición de problemas si la cantidad de estados es mucho menor a la cantidad de llamados recursivos. O sea, si 
$NP<< 2^{N} \leftrightarrow P<<2^{N}/N$
con N=|B|. 

## d) 
La idea sería tener una matriz de N*P posiciones. 

## e) 
```cpp
#include <iostream>
#include <vector>

using namespace std;

int infinito=1e9;
vector<int> b(0);
vector<vector<pair<int,int>>> memo;

//i=indice que veo; j=precio restante.
pair<int,int> traga_monedas (int i, int j) {
    if (i<0 && j>0) {
        return make_pair(infinito, infinito);
    }
    if (j<=0) {
        return make_pair(0,0);
    }
    if (memo[i][j].first != -1 || memo[i][j].second != -1) {
        return memo[i][j];
    }
    pair<int,int> con_billete_i = traga_monedas(i-1,j-b[i]);
    pair<int,int> sin_billete_i = traga_monedas(i-1, j);
    if (con_billete_i.first+b[i] == sin_billete_i.first) {
        if (con_billete_i.second < sin_billete_i.second) {
            memo[i][j] = make_pair(con_billete_i.first+b[i], con_billete_i.second+1);
        } else {
            memo[i][j] = make_pair(sin_billete_i.first, sin_billete_i.second);
        }
    } else if ((con_billete_i.first+b[i] < sin_billete_i.first)) {
        memo[i][j] = make_pair(con_billete_i.first+b[i], con_billete_i.second+1);
    } else {
        memo[i][j] = make_pair(sin_billete_i.first, sin_billete_i.second);
    }
    return memo[i][j];
}

int main() {
    int cant;
    cin >> cant;
    for (int i=0; i<cant; i++) {
        int elem;
        cin >> elem;
        b.push_back(elem);
    }
    int costo;
    cin >> costo;
    memo.resize(cant, vector<pair<int,int>>(costo+1, make_pair(-1,-1)));
    pair<int, int> res = traga_monedas(b.size()-1, costo);
    cout << res.first << ", " << res.second;
    return 0;
}
```

## f)
La llamada que resuelve el problema es traga_monedas(|B|-1, c). 
La nueva complejidad se calcula como la cantidad de estados posibles * complejidad de calcular cada estado. 
Complejidad = O(NP)
