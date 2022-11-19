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
