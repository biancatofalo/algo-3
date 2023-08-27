#include <iostream>
#include <vector>

using namespace std;

int min_costo() {
    
}

int main() {
    int cantCortes;
    cin >> cantCortes;
    vector<int> cortes(cantCortes);
    for (int i=0; i<cantCortes; i++) {
        int elem;
        cin >> elem;
        cortes[i]=elem; 
    }
    cout << "El menor costo para hacer los cortes es " << min_costo(); 
    return 0; 
}
