# Backtracking

Es una forma sistemática de recorrer todas las posibles configuraciones del espacio de soluciones. 

Las **configuraciones** incluyen por ejemplo todos los posibles conjuntos de disposiciones (permutaciones) o todos los posibles caminos para construir una colección de ellos (subconjuntos). 

Se debe generar cada configuración una sola vez. 
Para evitar esto, se debe establecer un orden entre todas las configuraciones. 

## Búsqueda exhaustiva

Con este método podemos resolver problemas pequeños encontrando la solución óptima, aunque la complejidad temporal sea enorme. 

Algunas veces se puede mejorar la búsqueda con métodos como el branch and bound o el branch and cut. 

## Búsqueda combinatoria

Representamos nuestras configuraciones con un vector: A (a1,...,an) donde cada elemento ai es seleccionado de un set ordenado de los posibles candidatos Si para una posición i. 

El procedimiento de búsqueda funciona aumentado las soluciones en un elemento en cada unidad de tiempo. 

En cada paso, una solución parcial (a1,...,ak) es construída. 

### Método

- Un conjunto candidato Sk+1 para una posición (k+1), es definido,

- Se intenta extender la solución parcial añadiendo el siguiente elemento de Sk+1. 

- Mientras la extensión mantenga una solución parcial más larga, la continuamos extendiendo. 

- En algún momento, Sk+1 = ∅, entonces, hacemos backtrack y remplazamos el último elemento ak, el último ítem en el valor de la solución, con el siguiente element en Sk. 

### Pseudocódigo

    procedure Backtrack(A,k)
        si A = (a1,...,ak) es solución entonces
            report it
        else 
            k = k+1
            calcula Sk
            While Sk /= ∅ 
                ak= elemento en Sk
                Sk= Sk - {ak}
                BacktrackR(A,k)

Cada llamada recursiva identifica un subproblema que es resuelto recursivamente.   

## Generando subsets

Sea S un set con n elementos
Hay un total de 2^n subconjuntos en total y n sobre k subconjuntos de k elementos. 

Si enumeramos todos los subconjuntos (p. ej. con un orden lexicográfico), el recorrido será un árbol de recursión en profundidad.

## Generando todas las permutaciones

Hay un total de n! permutaciones de un conjunto de n elementos. 
Hay n opciones para el primer elemento, n-1 para el siguiente, etc.

n! puede ser delimitado utilizando la fórmula de Stirling:

![Stirling's formula](https://johncarlosbaez.files.wordpress.com/2021/10/stirlings_formula-1.jpg?w=640)

El algoritmo realiza un recorrido en profundidad del árbol de configuraciones.

## El problema del viajante de comercio

*Problema*

Dadas n ciudades con distacias dij entre un par de ellas, encontrar el recorrido más corto que pasa exactamente una vez por cada ciudad.

*Primera idea*

Realizar backatracking generando todas las permutaciones y modificarla para computar la longitud de la permutación y devolver el mínimo. 

Este algoritmo produce el óptimo en O(n!d) donde n es el número de ciudades i d es la longitud de la distancia máxima. 

*Segunda idea*

Igual que antes pero descartados algunas soluciones parciales mayores que la solución actual (poda)- Se reduce pero tiene el mismo coste que el anterior.

## Knapsack

Tenemos un set I con n items y el ítem i tiene peso wi y un valor de vi. Tenemos un límite para transportar hasta un peso W. Considerando que no se pueden fraccionar los ítems:

*Primera idea*

Utilizar backtracking generando todos los subconjuntos.
Producirá el óptimo con coste (2^n * M) donde n es el número de objetos y M es la longitud máxima de los números en los inputs.

*Segunda idea*

Utilizar backtracking con poda para no generar todos los hijos en los que el peso supera W.
En caso peor, tiene el mismo coste que el anterior, exponencial. 

*Tercera idea*

Si encontramos una buena solución al inicio, excluyendo las soluciones parciales con coste menor menor, podemos reducir el tamaño de la búsqueda. 
El coste sigue siendo ifual que el anterior. 

*Quarta idea: Branch and bound*

Descartamos algunas ramas limitando la mejora
