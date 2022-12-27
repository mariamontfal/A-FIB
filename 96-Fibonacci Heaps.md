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

Potential Function:

$\Upphi$(H) = trees(H) + 2 * marks (H)


## Insert

- Crea un nuevo árbol solitario
- Lo añade a la lista de la raíz y actualiza el puntero del mínimo (si es necesario)

1) Coste real: O(1)

2) Cambio en la función potencial: +1

3) Coste amortizado: O(1)

## Delete Min

Operación de vinculación: hace que la raíz mayor sea hijo de una raíz menor. 
- Elimina el mínimo; une a sus hijos en la lista de la raíz; actualiza el mínimo.
- Consolida el árbol  para que dos raíces no tengan el mismo rank. 

1) Coste real: O(rank(H)) + O(trees(H))
- O(rank(H)) para unir los hijos del mínimo en la lista raíz
- O(rank(H) + O(trees(H)) para actualizar el mínimo
- O(rank(H) + O(trees(H)) para consolidar los árboles

2) Cambio en la función potencial: O(rank(H)) - trees(H)
- trees(H') $\leq$ rank(H) + 1 al no poder haber dos árboles con el mismo rank
- $\Updelta \Upphi$ (H) $\leq$ rank(H) + 1 - trees(H)

3) Coste amortizado: O(rank(H))

!! O(rank(H)) es un buen coste amortizado solo si $\leq$ lg n
Con las operaciones de insert y delete-min, como todos los árboles son binomiales, implica que O(rank(H)) $\leq$ lg n

Tenemos que implementar decrease-key para que O(rank(H)) = lg n

## Decrease key

Intuición para decrecer key del nodo x
- Si el orden del heap no es violado, simplemente decrementamos la key de x
- Sino, cortamos el árbol con raíz en c para unirlos en una lista de raíz
- Para mantener los árboles planos: tan pronto como un nodo tenga su segundo hijo cortado, cortamos y lo unimos en la lista de raíz (y lo desmarcamos)

1) Coste real: O(c)
- O(1) para cambiar la key
- O(1) para cada uno de los c cortes, + añadir a la lista de la raíz

2) Cambio en la función potencial: O(1) - c
- trees(H') = trees(H) + c
- marks(H') $\leq$ marks(H) + c
- $\Updelta \Upphi$ (H) $\leq$ c + 2 * (-c + 2)= 4 - c

3) Coste amortizado: O(1)

### Análisis

Insert:   		O(1)
Delete-min:   O(rank(H))  †
Decrease-key: O(1) †

† amortizado

Key Lemma: rank(H) = O(log n)
