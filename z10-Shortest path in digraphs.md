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

- Algoritmo que funciona para todo tipo de pesos y detecta si la distancia puede ser definida. 
-Supone que el grafo entra como una lista de adyacencia.

*Pseudocódigo:*

    BF (G,w,s):
        For v ∈ V , d[v] = +∞, p[v] =v
        d[s] = 0
        for i = 1 to n − 1 do:
            for all (u,v) ∈ E do:
                Relax(u, v)
        for all (u, v) ∈ E do:
            if d[v] > d[u] + w (u, v) then:
                return Ciclo con peso negativo
        return d, p

**Correctitud de BF:**

Consideramos el vector d computado por BF al final de la iésima iteración. Para v ∈ V, d[v] ≤ w(P) para cada camino P de s a v y longitud l(O) ≤ i. 

La demostración se hace con inducción sobre i. 

Antes de la iésima iteración, d[v] ≤ min{w(p)} para todos los caminos p con almenos i-1 aristas. 

La iésima iteración considera todos los caminos con ≤ i aristas alcanzando v, cuando se relaja la última arista en estos caminos. 

**Teorema:** Si (G,w) no tiene ciclos con pesos negativos, BF computa correctamente δ(s, v). 

Demostración:

- Sin ciclos con pesos negativos, el camino mínimo es simple (no repite vértices). Como mucho n vértices y n-1 aristas.

- Con el lema anterior, las n-1 iteraciones mantienen d[v] ≤ δ(s, v). 

- Por el invariante de relajación : d[v] ≥ δ(s, v). 

**Teorema:** BF encuentra el ciclo con peso negativo, si y solo si existe y es alcanzable desde s. 

Demostración:

- Sin ciclos con pesos negativos, el teorema anterior implica d[v] = δ(s, v), y por la desigualdad triangular d[v] ≤ δ(s, v) + w(u, v), por lo que BF no reportará un ciclo con peso negativo si no existe.

- Si existe un ciclo con peso negativo, entonces, una de las aristas puede ser relajada para que BF funcione correctamente. 

**Coste del algoritmo:** O (n*m)

#### DAGs

Dado un grafo G con aristar dirigidas con peso, G = (V,E,w) y s ∈ V, encontrar el camino mínimo de s al resto de vértices en G si existe. 

- Un DAG no tiene ciclos, por lo que la distancia puede ser definida entre cualquier par de vértices. 
- En particular, hay un camino mínimo de s a cualquier v alcanzable desde s. 
- Para obtener un algoritmo más rápido, miramos en una buena ordenación para las aristas: orden topológico. 


*Pseudocódigo:*

Sea Pre(v) = {u ∈ V | (u, v) ∈ E}
    

    
    SSSP-DAG(G , w):
        Sort V in topologica order
        For v ∈ V set d[v] = ∞ and p[v] = v
        d[s] = 0
        for all v ∈ V − {s} in order do:
            d[v] = min <sub>u ∈ Pre(v)</sub>{d[u] + w<sub>uv</sub>}
            p[v] = arg min<sub>u∈Pre[v]</sub>{d[u] + w<sub>uv</sub>}



**Complejidad**: T(n) = O(n+m)

**Correctitud**: d[u] = δ(s, u), para u ∈ Pre(v)

### All pairs shortest paths

- Dado un grafo G = (V,E,w), |V| = n, |E| = m,  queremos determinar ∀u, v ∈ V , δ(u, v).

- Asumimos que G no contiene ciclos con peso negativo. 
- Idea naive: aplicamos n veces BF o Dijkstra(si no hay pesos con cilo negativos). 
- La repetición de BF n veces tendría un coste de O(n<sup>2</sup>m). 
- La repetición de Dijkstra n veces tendría un coste de O(n * m * lg n) (si Q está implementado con un heap). 
- En vez de considerar la representación de G en una lista de adyacencia como en SSSP, aquí se considera la entrada como una matriz de adyacencia. 
- Por conveniencia V = {1,...,n}. La matriz de adyacencia n x n W = (w(i,j)) de G, w:

$$\ w_{ij} =
\begin{cases}
0 & si & i = j \\
w_{ij} & si & (i,j)\in E \\
\infty &  si  & i\neq j  \wedge (i,j) \notin E 
\end{cases}
\$$

- La salida es una matrix *n* x *n* D, donde D[i,j] = $\delta$ (i,j) y una matrix *n* x *n* P, donde P[i,j] es el predecesor de j en el camino mínimo de i a j.
    
    
Para resolver este problema tenemos dos estrategias diferentes:


#### Algoritmo de Floyd-Warshall

- Algoritmo que utiliza la programación dinámica para explotar la estructura recursiva de los caminos mínimos. Cada subcamino de un camino mínimo es un camino mínimo.
- Sea d<sub>ij</sub><sup>(k)</sup> el peso mínimo de un camino de i a j, sus nodos intermedios van de {1,...,k}. 
- Cuando k = 0, d<sub>ij</sub><sup>(0)</sup> = w<sub>ij</sub> (no hay nodos intermedios)
- Utiliza una matriz de adyacencia.

*La recurrencia:*

- Si k no es un nodo intermedio del camino p entre i y j, entonces d_{ij}^{(k)} = d_{ij}^{(k-1)}.
- Si k es un nodo intermedio de p, p se puede subdividir en i-> p1 k->p2j donde p1 y p2 son caminos mínimos con nodos intermedios {1,...k-1}

$$\ d_{ij}^{(k)} =
\begin{cases}
w_{ij} & si & k = 0 \\
min{d_{ij}^{(k-1)}, d_{ik}^{(k-1)} + d_{jk}^{(k-1)}} & si & k\geq 1 \\
\end{cases}
\$$


*Pseudocódigo:*
~~~
    BFW(W):
    d⁽⁰⁾ = W
    for k = 1 to n do:
        for i = 1 to n do:
            for j = 1 to n do:
                 d_{ij}^{(k)} = min{d_{ij}^{(k-1)}, d_{ik}^{(k-1)} + d_{jk}^{(k-1)}}
    return d^n
~~~


**Complejidad:**  O(n³)

**Correctitud:** De la recurrencia

Para construir la matriz P donde p<sub>ij</sub> es el predecesor de j con camino mínimo i-> j : 

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

- Algoritmo que funciona para todo tipo de pesos y detecta si la distancia puede ser definida. 
-Supone que el grafo entra como una lista de adyacencia.

*Pseudocódigo:*

    BF (G,w,s):
        For v ∈ V , d[v] = +∞, p[v] =v
        d[s] = 0
        for i = 1 to n − 1 do:
            for all (u,v) ∈ E do:
                Relax(u, v)
        for all (u, v) ∈ E do:
            if d[v] > d[u] + w (u, v) then:
                return Ciclo con peso negativo
        return d, p

**Correctitud de BF:**

Consideramos el vector d computado por BF al final de la iésima iteración. Para v ∈ V, d[v] ≤ w(P) para cada camino P de s a v y longitud l(O) ≤ i. 

La demostración se hace con inducción sobre i. 

Antes de la iésima iteración, d[v] ≤ min{w(p)} para todos los caminos p con almenos i-1 aristas. 

La iésima iteración considera todos los caminos con ≤ i aristas alcanzando v, cuando se relaja la última arista en estos caminos. 

**Teorema:** Si (G,w) no tiene ciclos con pesos negativos, BF computa correctamente δ(s, v). 

Demostración:

- Sin ciclos con pesos negativos, el camino mínimo es simple (no repite vértices). Como mucho n vértices y n-1 aristas.

- Con el lema anterior, las n-1 iteraciones mantienen d[v] ≤ δ(s, v). 

- Por el invariante de relajación : d[v] ≥ δ(s, v). 

**Teorema:** BF encuentra el ciclo con peso negativo, si y solo si existe y es alcanzable desde s. 

Demostración:

- Sin ciclos con pesos negativos, el teorema anterior implica d[v] = δ(s, v), y por la desigualdad triangular d[v] ≤ δ(s, v) + w(u, v), por lo que BF no reportará un ciclo con peso negativo si no existe.

- Si existe un ciclo con peso negativo, entonces, una de las aristas puede ser relajada para que BF funcione correctamente. 

**Coste del algoritmo:** O (n*m)

#### DAGs

Dado un grafo G con aristar dirigidas con peso, G = (V,E,w) y s ∈ V, encontrar el camino mínimo de s al resto de vértices en G si existe. 

- Un DAG no tiene ciclos, por lo que la distancia puede ser definida entre cualquier par de vértices. 
- En particular, hay un camino mínimo de s a cualquier v alcanzable desde s. 
- Para obtener un algoritmo más rápido, miramos en una buena ordenación para las aristas: orden topológico. 


*Pseudocódigo:*

Sea Pre(v) = {u ∈ V | (u, v) ∈ E}
    

    
    SSSP-DAG(G , w):
        Sort V in topologica order
        For v ∈ V set d[v] = ∞ and p[v] = v
        d[s] = 0
        for all v ∈ V − {s} in order do:
            d[v] = min <sub>u ∈ Pre(v)</sub>{d[u] + w<sub>uv</sub>}
            p[v] = arg min<sub>u∈Pre[v]</sub>{d[u] + w<sub>uv</sub>}



**Complejidad**: T(n) = O(n+m)

**Correctitud**: d[u] = δ(s, u), para u ∈ Pre(v)

### All pairs shortest paths

- Dado un grafo G = (V,E,w), |V| = n, |E| = m,  queremos determinar ∀u, v ∈ V , δ(u, v).

- Asumimos que G no contiene ciclos con peso negativo. 
- Idea naive: aplicamos n veces BF o Dijkstra(si no hay pesos con cilo negativos). 
- La repetición de BF n veces tendría un coste de O(n<sup>2</sup>m). 
- La repetición de Dijkstra n veces tendría un coste de O(n * m * lg n) (si Q está implementado con un heap). 
- En vez de considerar la representación de G en una lista de adyacencia como en SSSP, aquí se considera la entrada como una matriz de adyacencia. 
- Por conveniencia V = {1,...,n}. La matriz de adyacencia n x n W = (w(i,j)) de G, w:

$$\ w_{ij} =
\begin{cases}
0 & si & i = j \\
w_{ij} & si & (i,j)\in E \\
\infty &  si  & i\neq j  \wedge (i,j) \notin E 
\end{cases}
\$$

- La salida es una matrix *n* x *n* D, donde D[i,j] = $\delta$ (i,j) y una matrix *n* x *n* P, donde P[i,j] es el predecesor de j en el camino mínimo de i a j.
    
    
Para resolver este problema tenemos dos estrategias diferentes:


#### Algoritmo de Floyd-Warshall

- Algoritmo que utiliza la programación dinámica para explotar la estructura recursiva de los caminos mínimos. Cada subcamino de un camino mínimo es un camino mínimo.
- Sea d<sub>ij</sub><sup>(k)</sup> el peso mínimo de un camino de i a j, sus nodos intermedios van de {1,...,k}. 
- Cuando k = 0, d<sub>ij</sub><sup>(0)</sup> = w<sub>ij</sub> (no hay nodos intermedios)
- Utiliza una matriz de adyacencia.

*La recurrencia:*

- Si k no es un nodo intermedio del camino p entre i y j, entonces d_{ij}^{(k)} = d_{ij}^{(k-1)}.
- Si k es un nodo intermedio de p, p se puede subdividir en i-> p1 k->p2j donde p1 y p2 son caminos mínimos con nodos intermedios {1,...k-1}

$$\ d_{ij}^{(k)} =
\begin{cases}
w_{ij} & si & k = 0 \\
min{d_{ij}^{(k-1)}, d_{ik}^{(k-1)} + d_{jk}^{(k-1)}} & si & k\geq 1 \\
\end{cases}
\$$


*Pseudocódigo:*
~~~
    BFW(W):
    d⁽⁰⁾ = W
    for k = 1 to n do:
        for i = 1 to n do:
            for j = 1 to n do:
                 d_{ij}^{(k)} = min{d_{ij}^{(k-1)}, d_{ik}^{(k-1)} + d_{jk}^{(k-1)}}
    return d^n
~~~


**Complejidad:**  O(n³)

**Correctitud:** De la recurrencia

Para construir la matriz P donde p<sub>ij</sub> es el predecesor de j con camino mínimo i-> j : 

- Definimos la secuencia de matrices P⁽⁰⁾, P⁽¹⁾, ..., P<sup>(n)</sup>. p<sub>{i,k}</sub><sup>k</sup> es el predecesor con camino mínimo i-> j el cual utiliza nodos en {1,..,n}. 


$$\ p_{ij}^{(0)} =
\begin{cases}
NIL & si & i = j \vee w_{ij} = \infty \\
i & si & i \neq j \wedge w_{ij} \neq \infty \\
\end{cases}
\$$

Para k \geq 1 tenemos la recurrencia:

$$\ p_{ij}^{(k)} =
\begin{cases}
p_{ij}^{(k-1)} & si & d_{ij}^{(k-1)} \leq d_{ik}^{(k-1)} + d_{kj}^{(k-1)} \\
p_{kj}^{(k-1)} & sino \\
\end{cases}
\$$

**Complejidad con caminos:** queda igual ya que solo se debe añadir la línea correspondiente de p para actualizarla en el código anterior. Por tanto, O(n³).


#### Algoritmo de Johnson

- Algoritmo más eficiente para grafos dispersos, donde m = o(n²). 
- El grafo entra como una lista de adyacencia y asumimos que no existen ciclos con peso negativo. De hecho, el algoritmo detecta su existencia.
- EL algoritmo utiliza BF para reducir el problema a uno con pesos positivos. 
- Entonces, ejecuta n veces el algoritmo de Dijkstra.

*Modificación de peso que preserva los pesos de los caminos:*

Sea G = (V,E,w) un grafo dirigido con pesos. Sea f : V → $\mathbb{R}$ y para cada (u,v) $\in$ E, sea w'(u,v) = w(u,v) + f(u) - f(v). Sea p un camino de u a v en G, entonces w'(p) = w(p) + f(u) - f(v).

Para hacer esta modificación definimos G' añadiendo al grafo G un nuevo vértice s y aristas (s,u) para u $\in$ V. Definimos w'(e) = w(e) si E' $\cap$ E y 0 sino. 

- Sea d la salida para BF con entrada (V',E',w',s)
- Si G no tiene pesos negativos, G' no tiene pesos negativos, así que BF computa d: V → $\mathbb{R}$. Además, para cada u $\in$ V, d(u) = $\delta\$<sub>G'</sub>(s,u).

**Lema:**

Sea G = (V,E,w) un grafo dirigido con pesos sin ciclos con peso negativo. Sea d: V → $\mathbb{R}$ la función que computa con BF en G' descrita. Sea G<sub>d</sub> = (V,E,w') donde w'(u,v) = w (u,v) + d(u) - d(v). 
Si p es el camino más corto de u a v en G, p es el camino más corto en G<sub>d</sub>. Además $\delta$<sub>G<sub>d</sub></sub>(u,V) = $\delta$<sub>G</sub> + d(u) - d(v).  

*Demostración:*

Para cada camino p de u a v, w'(p) = w(p) + d(u) - d(v). El último término depende solo de u y de v. 

Por la desigualdad triangular, el camino p de u a v, δ<sub>G'</sub>(s, v) ≤ δ<sub>G'</sub>(s, u) + w(p). Entonces, w'(p) = w (p) + d(u) − d(v) ≥ 0

*Pseudocódigo:*

    Johnson (V , E , W)
        Compute G'
        f = BF (G', s)
        Compute Gf
        for all v ∈ V do:
            d[v] = Dijkstra(Gf , v)
        for all u, v ∈ V do:
            d[u][v] = d[u][v] + f [v] − f [u]
        return d

**Complejidad:** O(n * m) + coste de n llamadas a Dijkstra.

### Conclusiones

#### SSSP

|                          |     Dijkstra     |        BF        |
|--------------------------|------------------|------------------|
| w $\geq$ 0                 |  O(m + n * lg n)   | O(n * m)         |
| w $\in$   $\mathbb{Z}$    |   NO             | O(n * m)         |

#### APSP
|                   |   Dijkstra   |    BF    |  FW |    Johnson    |
|--------------------------|------------------|------------------|----|----|
| w $\geq$ 0                 | O(n * m + n² * lg n)  | O(n² * m)         | O(n³) | O(n * m + n² * lg n) 
| w $\in$   $\mathbb{R}$   |   NO             | O(n² * m)         | O(n³) | O(n * m + n² * lg n)


*Algunos puntos sobre APSP:*

- Para grafos dispersos con m = ω(n), m = o(n²), Johnson es el más eficiente.

- Para grafos densos con m =  Θ(n²), FW tiene la mejor complejidad. 

- Para grafos no dirigidos o sin pesos, hay un algoritmo de R.Seidel que trabaja en tiempo O(n<sup>ω</sup>lg n), donde n<sup>ω</sup> es la complejidad de multiplicar dos matrices *n* x *b* donde <sup>ω</sup> ~ 2.3.
