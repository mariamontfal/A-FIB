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

Utiliza un union-find como estructura de datos. 
