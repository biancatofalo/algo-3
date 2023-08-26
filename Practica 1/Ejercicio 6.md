### Ejercicio 2
## a) 
* (infinito, infinito) si i=|B| ^ j>0
* (0,0) si j<0
* min(cc({b2,...,bn}, c-b1).first+b1, cc({b2,...,bn}, c-b1).second+1), (cc({b2,...,bn}, c-b1).first, cc({b2,...,bn}, c-b1).second)))

## c) 
```cpp
#include <iostream>
#include <vector>

using namespace std;

int costo;
int infinito=1e9;

//i=indice que veo; j=precio restante
pair<int,int> traga_monedas (vector<int>& b, int i, int j) {
    if (i==b.size() && j>0) {
        return make_pair(infinito, infinito);
    }
    if (j<=0) {
        return make_pair(0,0);
    }
    pair<int,int> con_billete_i = traga_monedas(b, i+1, j-b[i]);
    pair<int,int> sin_billete_i = traga_monedas(b, i+1, j);

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
    pair<int, int> res = traga_monedas(billetes, 0, costo);
    cout << res.first << ", " << res.second;
    return 0;
}
```
