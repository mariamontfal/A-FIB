# Árboles generadores mínimos

### **Árboles:**

*Propiedades*
    -  Un árbol de n nodos tiene n-1 aristas.
    - Cualquier grafo no dirigido conexo con n vértices y con n-1 aristas es un árbol. 
    - Un grafo no dirigido es un árbol si y solo si tiene un camino único entre cualquier par de nodos.
    - Cualuquier grafo conexo tiene un árbol generador. 
    
#### **Problema del árbol generador mínimo**

Dada una entrada con un grafo con pesos G = (V,E,w), donde w:E->R.

Encontrar un árbol T = (V,E´) con E´⊆ E, tal que minimice la suma de los pesos de las aristas del árbol.

    Un MST T en G tiene las siguientes propiedad:
        - Cut property: e ∈ T <-> e es la arista menos pesada en algun corte de G
        - Cycle property: e /∈ T <-> e es la arista más pesada en algun ciclo de G
        
El algoritmo MST utiliza dos normas para añadir/descartar nodos

    1) La implicación hacia la izquierda de la propiedad de corte, sostiene la norma azul, la cual permite incluir de forma segura en T una arista mínima para algun corte identificado.
    
    2) La implicación hacia la derecha de la propiedad del ciclo, permite excluir de T la arista más pesada de un ciclo identificado.
    
#### **Implementaciones del MST problem:**

##### **Prim (serial centralized):**

Empezando desde un vértice v, hacer crecer T añadiendo en cada tiempo la arista de menos peso aún conexa a un vértice en T, (usando la regla cut).

Utiliza una cola de prioridad.

El algoritmo mantiene un árbol y añade una arista (y un nodo) a T en cada paso. 

Inicialmente el árbol T tiene un nodo arbitrário r y no tiene arista. 
En cada paso T se agranda añadiendo la arista de mínimo peso en C(T) = corte - conjunto (V(T,V-V(T))).

Notad que una arista e esta en el conjunto de corte si e tiene un final en V(T) y el otro fuera. 


*Pseudocódigo:*

    MST(G,w,r):
        //Nodo trivial r
        T = ({r},∅); Q = ∅; s = 0;
        Añadir en Q todas las aristas e = (r,v) con clave w(r,v)
        while s<n-1 && Q ¬empty do:
            (u,v,w) = Q.pop()
            si u ∈/ V(T) || v ∈/ V(T) entonces
                Sea u′ el vertex desde (u,v) que no está en T 
                Añadir en Q todas las aristas e = (u′,v′) ∈ E(G) 
                para v′ ∈/ V(T) con clave w(e)
                add e to T; ++s
            end si
        end for

Si Q es un heap el coste es: T(n) = O(|E|lg|V|).

##### **Kruskal (serial distributed):**

Considera cada nodo, en orden ascendiente de peso, para hacer crecer el bosque utilizando la regla de cut y la regla de ciclo. El algoritmo acaba cuando pasa de bosque a árbol. 

El algoritmo de Kruskal evoluciona construyendo bosques generadores y uniendo dos árboles (regla de corte) o descartando una arista (regla del ciclo). 

La propiedad conexa es una relación de equivalencia uRv sii existe un camino entre u y v.

Kruskal empieza con n particiones y acaba con una partición de V conjunta
.
Utiliza un union-find como estructura de datos. 

###### **Union-Find:**

*Características:*

Es una estructura de datos para mantener una partición dinámica de un conjunto. 

Es una de las estructuras de datos más elegantes en las herramientas algoritmicas. 

Hace posible diseñar algoritmos cuasi-lineales para problemes que sino serían inabordables. 


*Operaciones*

1. Makeset(x): 
    
    Crea un nuevo set con un solo elemento x.

2. Union(x,y):
    
    Fusiona los sets que contienen x e y utilizando su union.
    Consideramos Union(x,y) = Union(find(x),find(y)).

3. Find(x):
    
    Devuelve el representante del set que contiene x. 

*Pseudocódigo de Kruskal utilizando Union-Find*

    MST(G(V,E),w,r), |V|=n, |E|=m:
        Ordenar E en orden ascendiente por peso: {e1,..,em}
        T = ∅
        //Crea un set para cada vértice
        for all v ∈ V do
            MAKESET(v)
        end for
        for i=1 to m do
            ei=(u,v)
            if FIND(u)/=FIND(v) then
                T=T ∪ {ei}
                UNION(u,v)
            end if
        end for

Ordenar tiene coste O(m*log n)

El resto de código tiene cosete lineal en n para el MAKESET y O(m) operaciones del tipo FIND/UNION

El coste del algoritmo de Kruskal es O(m*lg m) = O(m* lg n) por la parte de ordenamiento, a no ser que utilicemos un rango de pesos que nos permita usar RADIX.

*Algunas aplicaciones para Union-Find*

    - Algoritmo de Kruskal para MST
    - Detección de ciclos en grafos no dirigidos
    - Estrategias para juegos: Hex y Go
    - Equivalencia de DFA's
    - Antecesor menor común
    - Connectividad dinámica de un grafo para grandes redes
    - Generación y exploración aleatoria de laberintos
    - Compilación de declaraciones de equivalencia
    
*Clustering:*

Proceso de encontrar una estructura interesante en un conjunto de datos. 

Dada una colección de objetos, organizarlos en grupos coherentemente similares con respecto a alguna función de distancia. 

La función de distancia no necesariamente debe ser una distancia Euclidea, sino una función de similitud respecto algun aspecto. 

*Algoritmo para el single-link clustering problem*

    - Aplicar el algoritmo de Kruskal hasta conseguir un bosque con k árboles. 
    Resuelve el problema en tiempo O(n^2 * lg n) ya que se tiene que crear el grafo completo y ordenar n^2 aristas. 
