# Shortest paths in digraphs

## Distances and shortest paths

Dado un digrapfo G = (V,E) con aristas con peso w: E → R

*Camino:*

- Un camino es una secuencia de vertices p = (v0,...,vk) la cual (vi,vi+1) ∈ E, para 0 ≤ i < k. 

- Un camino p = (v0,...,vk) tiene longitud l(p) = k y peso w(p) = Σ de i=0 a i = k-1 de w(vi, vi+1).

- Para un camino p = {u,...,v}, escribimismo u ->(p) v para decir que empieza en u y acaba en v. 

- Un camino permite vértices repetidos.

#### *Definiciones*

*Distancia:*

- Queremos asociar un valor para la distancia δ(u,v) para cada pareja de pares u, v en un digrafo con pesos (G,w), calculando el peso mínimo entre todos los caminos de u a v.

- Tenemos dos casos:
    
    1. Que no haya camino entre u y v, por lo que δ(u,v) = +∞.
    2. Que haya caminno entre u y v, por lo que la distancia será el min{w(p) | u->(p) v}. 

De otro modo, la distancia no puede ser definida. 

- **Teorema:** La distancia entre todos los pares u, v ∈ V (G) puede ser definida si y solo si, G no tiene ningún ciclo con peso negativo. En este caso, podrían definirse algunas distancias entre algunos pares, pero no todas. 

- Si G es no dirigido, consideramos cada arista en los dos sentidos y asignamos el mismo peso en ambas direcciones. 

- Si G no tiene pesos, podemos asignar a cada atista peso = 1. 

#### *Propiedades*

Dado G = (V,E,w), para cada p camino mínimo de u a v y para cada par de vértices i,j en el camino p, el subcamino p' de i a j de p es un camino mínimo.

- **Teorema:** Sea G = (V,E,w) el grafo tal que para u, v ∈ V, δ(u,v) puede ser definida. Para u,v,z  ∈ V(G), δ(u,v) ≤ δ(u,z) + δ(z,v).

Dado G = (V,E,w) un distinguido s ∈ V, un camino árbol mínimo es un subárbol dirigido, Ts = (V′,E′), de G.

- Ts tiene como raíz s
- V' es un conjunto de vértices en G alcanzables desde s
- Para v ∈ V′ el caminon de s a v en Ts tiene peso δ(s,v)


### Single Source shortest path

Dado un grafo G = (V,E,w) y s ∈ V, encontrar el camino mínimo de s al resto de vértices en G si este existe. 
- El algoritmo mantiene para v ∈ V, una sobreestimación de d[v] de δ(s,v) y un predecesor a candidato p[v] para el camino mínimo entre s y v. 

- Inicialmente, d[v] = +∞ para v ∈ V - {s}, d[s] = 0 y p[v] = v.

- Repetidamente, se mejora la estimación hasta llegar que d[v] = δ(s,v).

- En la arista seleccionada (u,v) ∈ E aplicar una operación de relajación.
    

    Relax (u,v):
        if d[v] > d[u] + w(u,v) then
            d[v] = d[u] + w(u,v)
            p[v] = u
            
Es decir d'[v] = min{d[v], d[u] + w(u,v)} } ≥ δ(s,v).

Para resolver este problema tenemos dos estrategias diferentes:

#### Algoritmo de Dijkstra

- Algoritmo greedy muy eficiente; en cada paso para un vértice v, d[v] se convierte en δ(s,v) con una distancia correcta.
- Solo funciona con **pesos positivos**.
- Supone que el grafo entra como una lista de adyacencia.
- Relaja las aristas correspondientes al vértice actual. 
-Utiliza una cola de prioridad.

*Pseudocódigo:*

    Dijkstra(G,w,s):
        d[u] = +∞ y p[u] = u, u ∈ V
        d[s] = 0
        S = ∅
        Insertar los vértices en Q con clave d
        while Q /= ∅ do:
        u = Q.pop()
        S = S ∪ {u}
        for all v ∈ Adj[u] y v /∈ S do:
            Relax(u, v)
            Cambiar la clave de v si es necesario

**Teorema:**

Considera S en cualquier punto de la ejecución del algoritmo. Para cada u ∈ S, d[u] = δ(s,u). 

La demostración es con inducción sobre |S|.

Utilizando una cola de prioridad, Dikstra puede ser implementado en un grafo con n nodos y m aristas en tiempo O(m) + el tiempo de los pops de la cola de prioridad y el cambio de clave. 

**Coste del algoritmo:**
- Con implementación de Q como un heap = O (m * lg n)
- Con implementación de Q como un Fibonacci heap = O (m + n + lg n)

#### Algoritmo de Bellman-Ford

Algoritmo que funciona para todo tipo de pesos y detecta si la distancia puede ser definida. 
Supone que el grafo entra como una lista de adyacencia.

### All pairs shortest paths

Dado un grafo G = (V,E,w) sin ciclos con peso negativo, para cada u,v ∈ V (G) encontrar el camino mínimo de u a v si existe. 

Para resolver este problema tenemos dos estrategias diferentes:


#### Algoritmo de Floyd-Warshall

Algoritmo que utiliza la programación dinámica y tiene como input la matriz de adyacencia de G.

#### Algoritmo de Johnson

Algoritmo eficiente para grafos dispersos. 

