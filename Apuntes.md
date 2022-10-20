# Introducción

### **Algoritmo:**

*Definición*
    
    Receta precisa para una tarea computacional. 
    
    Cada paso debe ser claro, inambiguo, y debe siempre llevar a una clara respuesta.
    
*Características deseables para la justificación de un algoritmo*

    - Correctitud: siempre hace lo que debe hacer.
    
    - Performance: tiempo de ejecución, memoria en uso, costes de comunicación...
    
    Siempre analizaremos el coste teniendo en cuenta el peor caso.



### **Grafos:**

*Definición*
    
    Sea G un grafo tal que G = (V,E), donde V es el nopmbre de vértices y E es el set de aristas 
    tales que son un subconjunto de VxV. 
    
    Definimos n como el número de vértices y m como el número de aristas. 
    
*Algunas propiedades*

    - Dirigidos / No dirigidos.
    
    - El grado de un vértice v es el número de aristas incidentes en v.
    
    - Una clique en n vértices (Kn) es un grafo completo con m = n*(n-1)/2.
    
    - Un grado no dirigido es conexo si hay un camino entre dos vértices cualesquiera.
    
    - Si G es conexo, entonces m>= n-1.
    
    - Un grafo G en denso cuando m = Θ (n^2).
    
    - Un grafo G es disperso cuando m = o (n^2).
    
    
    
*Grafos dirigidos*

    - Las aristas tienen dirección. 
    
    - El concepto conexo de digrafos es también llamado fuertemente conexo. 
      Hay un camino dirigido entre cualquier par de vértices.
      
    - En un digrado: m <= n(n-1). 
    
*Matriz de adjacencia y lista de adjancencia*

1) Representación
    - El espacio para representar la lista es: Θ(n+m)
    - El espacio para representar la matriz es: Θ(n^2)
    
    En general, para grafos sin pesos y densos, la matriz tiende a ser una representación mejor. 
    Sino, la lista es una representación más concisa. 
    
2) Complejidad
    
    - Añadir una nueva arista en G: Θ(1) en ambas estructuras.
    - Consultar si una arista está en el grafo: Θ(1) en la matriz y O(n) en la lista.
    - Explorar todos los vecinos de un vértice: Θ(n) en la matriz y Θ(|d(v)|). 
    - Borrar una arista: Θ(1) en la matriz y O(n) en la lista.
    - Borrar un vértice: Θ(n) en la matriz y O(m) en la lista.
    
    
### **Breadth First Search and Depth Search Search**

*Pseudocódigo BFS*:
    
    1) Empezar con el vértice v, visitar v y todos sus vecinos. 
    2) Después, visitar los vecinos no visitados, de los vértices ya visitados. 
    3) Repetir hasta visitar todos los vértices
    
BFS utiliza una cola (FIFO), para mantener a todos los vecinos de los vértices visitados. 



*Pseudocódigo DFS*:
    
    1) Del vértice actual, pasamos a su primer vecino.
    2) Repetir 1 hasta que no se pueda. 
    3) Entonces, backtrack hasta un nodo no visitado. 
    
DFS utilizado una cola (LIFO)



**Tanto para DFS como para BFS la complejidad es:**
    
    - O(|V|+|E|) si la representación de G está con lista de adjancencia.
    - O(|V|^2)   si la representación de G está con matriz de adjancencia.



### **Componentes conexas en grafos no dirigidos**

Una componente conexa es una subgrafo maximal conexo de G. 


Un grafo conexo tiene una única componente conexa. 

    - Para encontrar una componente conexa en G, utilitzar el DFS para mantener 
      el seguimiento del conjunto de vértices visitados en cada llamada exploradora. 
      El problema puede ser resuelto en O(|V|+|E|).
      
### **Componentes conexas en grafos dirigidos**

Un digrafo tiene una componente fuertemente conexa, si para todo vértice u,v 

perteneciente a V, existe un camino que va de u a v y de v a u. 

El grafo de la componente fuertemente conexa SIEMPRE será acíclico. 


Una componente fuertemente conexa, es una componente maximal fuertemente conexa del grafo. 


#### ***Kosharaju-Sharir's algorithm***

Utiliza dos DFS para resolver el problema. 

*Complejidad*:  O(|V|+|E|)

*Pseudocódigo*:

    1) Crear una pila vacía.
    2) Ejecutar DFS. Durante el recorrido DFS, después de invocar al DFS recursivo.
        2.2) Para cada vértice adjacente al vértice actual, hacer push del vértice en la pila. 
    3) Girar las aristas para conseguir el grafo traspuesto. 
    4) Uno a uno, eliminar cada vértice de la pila mientras esta no sea vacía. 
        Sea v el vértice eliminado, aplicar DFS sobre v. 
        El DFS empezando por v generará las componentes fuertemente conexas de v.

#### ***Tarjan's algorithm***

Utiliza un DFS para resolver el problema. 

*Complejidad*:  O(|V|+|E|)

*Pseudocódigo*:

    1) Actualizar el contadorVisita y el tiempo del vértice actual
    2) Hacer push en la pila
    3) Para cada vértice adjacente al vértice actual:
        3.1) Si el vértice no había sido visitado, llamar recursivamente a la función. 
        3.2) Si el vértice ya estaba en la pila (backedge), actualizamos el valor de low
        
### **P y NP**

*Vertex Cover*

    Problema: dado un grafo G = (V,E), con |V| = n y |E| = m, encontrar el conjunto
    mínimo de vértices que cubre cada arista del grafo G.
    
    Es un problema de complejidad NP-Hard.
    
*Set Cover*

    Problema: Dado un conjunto U de m elementos, una colección S = {S1,...Sn} donde
    Si es subconjunto de U, seleccionar el mínimo número de subconjuntos tales que 
    su unión es igual a U. 
    
    Es un problema de complejidad NP-Hard.
    
Vertex Cover es un caso especial del problema Set Cover. 

    
