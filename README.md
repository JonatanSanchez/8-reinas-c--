8-reinas-c--
============

El problema de las ocho reinas es un juego que consiste en colocar ocho reinas en un ajedrez sin que se amenacen entre sí.  La solución a este problema se encuentra con un algoritmo de backtracking, que consiste en asignar una fila a cada reina, y progresivamente colocar cada reina en una posición diferente. 

#include <iostream>
#include <sstream>
#include <cstdio>
#include <vector>
#include <algorithm>
#define NREINAS 8 // dimensiones del tablero y número de reinas
using namespace std;
vector<int> sol;
int nro_sol=1;
 
 
inline bool contiene(const vector<int>& v, const int val)
{
    return find(v.begin(), v.end(), val) != v.end();
}
 
void reinas(int k, vector<int> col, vector<int> diag45, vector<int> diag135)
{
    if( k == NREINAS )
    {
	printf("%3d:", nro_sol++);
        for(int j=0; j<NREINAS; j++)
	    cout << " (" << j+1 << "," << sol[j] << ")";
        cout << endl;
    }
    else
    {
        for(int j=1; j<=NREINAS; j++)
            if( !contiene(col, j) && !contiene(diag45, j-k) && !contiene(diag135, j+k) )
            {
                sol[k] = j;
 
                col.push_back(j);
                diag45.push_back(j-k);
                diag135.push_back(j+k);
 
                reinas(k+1,col, diag45, diag135);
 
                col.pop_back();
                diag45.pop_back();
                diag135.pop_back();
            }
    }
}
 
int main() {
    cout << "SOLUCIONES AL PROBLEMA DE LAS " << NREINAS << " REINAS";
    sol.resize(NREINAS);
    reinas(0, vector<int>(), vector<int>(), vector<int>());
 
    return 0;
