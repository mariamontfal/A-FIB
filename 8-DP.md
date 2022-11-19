# DP

Poderosa técnica para implementar eficientemente algoritmos recursivos guardando resultados parciales y reutilizándolos cuando son necesarios. 

#### Características:

1) *Subproblemas:* debe haber una forma de partir el problema global en subproblemas, cada uno con una estructura similar al original pero de menor tamaño. 

2) *Subestructura óptima:* una solución óptima debe componerse de soluciones óptimas a subproblemas, utilizando una combinación relativamente simple. 

3) *Subproblemas repetidos:* el algoritmo recursivo resuelve un número pequeño distinto de subproblemas, pero estos son repetidamente resueltos. 

Por la última propiedad se puede sacar partido de la memoización; se guardan los valores utlizando una estructura apropiada y se reutlizan cuando es necesario. 

#### Diferencia con los algoritmos greedy:

Los algoritmos greedy utilizan la propiedad de la opción greedy, escogen un óptimo local para dirigir a una solución globalmente óptima. Es decir, se resuelve recursivamente un subproblema. 

En programación dinámica, se resuelven todos los posibles subproblemas.

#### Diferencia con divide y vencerás:

Divide y vencerás parte el problema con una fracción del tamaño del problema original (size/b).

En programación dinámica se divide el problema en subproblema con el mínimo tamaño, pero a menudo, sin ser una fracción del tamaño original. 

#### Cálculo del iésimo número de Fibonacci

Si se implementa recursivamente el subproblema del iésimo número de fibonacci es repetido muchas veces en diferentes llamadas recursivas. 

*Implementación con programación dinámica:*

Aprovechamos el cálculo y lo guardamos en una estructura de datos para poder accederlo sin necesidad de calcularlo en todas las llamadas. 

    DP-Fibonacci (n) {Construir la tabla}:
        F[0] = 0
        F[1] = 1
        for i = 2 to n do:
            F[i] = F[i-1] + F[i-2]
            return F[n]
        
Para obtener Fn necesitamos O(n) en tiempo y espacio.

Podemos reducir el espacio a O(1) guardando solo los valores que necesitaremos en la siguiente iteración. 

Es un algoritmo pseudopolinomial ya que tiene tiempo de cómputo polinomial para valores de algunos parámetros de la entrada. 

### Guía para la resolución de problemas de PD

1) Caracterizar la estructura de los subproblemas: comprobar que el espacio de los subproblemas no es exponencial. Definir las variables. 

2) Definir recursivamente el valor de la solución óptima: encontrar la correcta recurrencia, con una solución para un problema más grande en función de las soluciones a los subproblemas. 

3) Cómputo, memoización/bottom-up, el coste de la solución: utilizando la fórmula recursiva, tabular solución a problemas más pequeños, hasta llegar a un valor para el problema completo. 

4) Construir una solución óptima: computar información adicional para hacer el seguimiento desde la solución óptima hasta el valor óptimo. 

#### Weighted activity selection problem

Conjunto S = {1,2,...,n} de actividades para ser procesadas por un único procesador. Cada actividad i tiene un tiempo de inicio si y un tiempo de finalización fi, con fi>si y con peso wi. Encontrar el conjunnto mutuamente compatible de actividades tales que maximiza la suma de sus pesos. 

Necesitamos tiempo O(n*lg n) para ordenar.

Tenemos O(n) subproblemas ya que en WAS-2(S, i) S mantiene el seguimiennto del valor de la solución e i define el subproblema para 0<=i<=n.

Definimos p(i) como el entero más grande j j<i y tal que i y j son disjuntas:

    - p(i) = 0 si no existe j disjunta
    - j<i si existe
    
Sea Opt(j) el valor para una solución óptima Oj para el subproblema consistente en las actividades comprendidas entre 1 y j.

*Recurrencia:*

Opt(j):

    - 0 si j = 0
    - max {(Opt(p[j]) + wj) , Opt[j-1]} si j>=1
    
*Correctitud:*

Tenemos dos casos:

**1. j ∈ Oj:**

- Como j pertenece a la solución, no pueden pertenecer a Oj (p(j)+1,...,j-1)

- Oj - {j} debe ser una solución óptima para {1,...,p[j]}, sino O'j = Op[j] ∪ {j} sería mejor (propiedad de subestructura óptima)

**2.j /∈ Oj:**
- Entonces Oj es una solució óptima para {1,...,j-1}

*Preprocesado*

1. Ordenar las actividades por orden creciente según fi. 

2. Computar los valores para p[i]
    
    Ordenar las actividades por orden creciente de si
    Fusionar la lista de tiempos de finalización y tiempos de inicialización, en caso de empate poner antes la de tiempo de finalización mínimo. 
    
3. Podemos computar los p valores en:
    O(nlgn + n) 
    
#### 0-1 Knapsack

Dado un conjunto de n ítems de entrada que no pueden ser fraccionados, el ítem i tiene peso wi y valor vi, y existe W como indicador del peso máximo permitido. 

Dividimos el problema:

Para computar v[i,x] hay dos posibilidades para ser consideradas con peso total <=x:

1. 0 si i = 0 o w = 0

2. max v[i-1,x-wi] + vi, v[i-1, x] sino

*Algoritmo: *

Definimos una tabla P[n+1, W+1] para mantener los valores óptimos de los subproblemas correspondientes. 
    
    Knapsack(i,x): 
        for i=0 to n do:
            P[i,0] = 0
        for x = 1 to W do:
            P[0,x] = 0 
        for i = 1 to n do:
            for x = 1 to W do:
                P[i,x] = max{P[i − 1,x], P[i − 1,x − w[i]] + v[i]}
        return P[n,W]
        
El número de pasos es O(nW) que es pseudopolinomial.

