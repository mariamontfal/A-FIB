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


