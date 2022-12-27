## Fibonacci Heaps

**Teorema:**

Utilizando un heap de Fibonacci, cualquier secuencia de a<sub>1</sub> insert, a<sub>2</sub> delete-min y a<sub>3</sub> decrease-key operaciones tinen un coste temporal de:
O(a<sub>1</sub> + a<sub>2</sub> log n + a<sub>3</sub>)

### Historia

[Fredman y Tarjan, 1986]
- Estructura de datos ingeniosa y análisis
- Motiviación original: mejorar algoritmo del camino mínimo de Dijkstra de O(E log V) a O(E + V log V)

Idea básica:
- Similar a los heaps binomiales, pero siendo una estructura de datos menos rígida.
- Binomial heap: consolidar árbels después de cada insert. 
- Fibonacci heap: diferir perezosamente la consolidación hasta el siguiente delete-min. 

### Estructura

- Conjunto de árboles de heaps ordenados: cada padre mayor a sus hijos
- Mantener el puntero al elemento mínimo: encontrar el mínimo requiere tiempo constante
- Conjunto de nodos marcados: utilizados para mantener los heaps planos

**Notación:**
- n         = número de nodos en el heap
- rank(x)   = número de hijos del nodo x
- rank(H)   = max rank de cualquier nodo en el heap H
- trees(H)  = número de árboles en el heap H
- marks(H)  = número de nodos marcados en el heap H

$\Upphi$(H) = trees(H) + 2 * marks (H)
