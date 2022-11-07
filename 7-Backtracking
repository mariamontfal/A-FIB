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
