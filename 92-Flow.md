## Max-flow and min-cut problems

Una red $\eta$ = *(V,E,c,s,t)* está formada por:

- Un digrafo G = (V,E), 
- Un vértice fuente s $\in$ V
- Un vértice sumidero t $\in$ V
- Capacidades para las atistas c: *E* $\rightarrow$ $\mathbb{R^+}$

**Un flujo en una red**

Dada una red $\eta$ = *(V,E,c,s,t)*.

Un flujo es una asignnación *f*: *E* $\rightarrow$ $\mathbb{R^+}$ $\cup$ {0} que sigue la regla de Kirchoff:

- $\forall$ (u,v) $\in$ E, 0 $\leq$ f(u,v) $\leq$ c(u,v)
- Conservación de flujo: $\forall$ v $\in$ V - {s,t}, $\Sigma$ <sub> u∈V </sub> f(u,v) = $\Sigma$ <sub> z∈V </sub> f(v,z)

El valor de flujo *f* es:

|f| = $\Sigma$ <sub> v∈V </sub> f(s,v) = f(s,V) = f(V,t)

****

### Problema del flujo máximo

Entrada: Una red $\eta$ = *(V,E,c,s,t)*

Objetivo: Encontrar el flujo de máximo valor en $\eta$

Dada una red $\eta$ = *(V,E,c,s,t)* un (s,t)-corte es una partición de *V = S* $\cup$ *T* ( *S* $\cap$ *T* = $\emptyset$), con s $\in$ S y t $\in$ T 

La capacidad de un corte (*S,T*) es la suma de pesos dejando *S*, por ejemplo c(*S,T*) =  $\Sigma$ <sub> u∈S </sub> $\Sigma$ <sub> v∈T </sub> c(u,v)

El flujo a través del corte:

*f(S,T)* = $\Sigma$ <sub> u ∈ S </sub> $\Sigma$ <sub> v ∈ T </sub> *f(u,v)* - $\Sigma$ <sub> v ∈ T </sub> $\Sigma$ <sub> u ∈ S </sub> *f(u,v)*

Por la restricción de capacidad: *f(S,T)* $\leq$ *c(S,T)*


****

### Problema del corte mínimo

Entrada: Una red $\eta$ = *(V,E,c,s,t)*

Objetivo: Encontrar el corte (s,t) de capacidad mínima en $\eta$

Si modificamos la entrada añadiendo c > 0 a la **capacidad de cada arista**, puede pasar que (S,T) ya no sea un corte (s,t) mínimo. 

**Efectos de cambiar el peso:**

Si modificamos la red multiplicando por c > la capacidad de cada arista, la capacidad de cualquier (s,t) corte en la nueva red es c veces la capacidad de la red original. 



****

### Propiedades de los flujos y cortes



#### Notación

Sea $\eta$ = *(V,E,c,s,t)* y *f* un flujo de $\eta$

Para v $\in$ V, 
U ⊆ V y v $\notin$ U:

- *f(v,U)* flujo v → U por ejemplo *f(v,U)* = $\Sigma$ <sub> u ∈ U </sub> *f(v,u)*

- *f(U,v)* flujo U → v por ejemplo *f(U,v)* = $\Sigma$ <sub> u ∈ U </sub> *f(u,v)*

Para un corte-(s,t) y v $\in$ S:

- S' = S \ {v} y T' = T $\cup$ {v}

- *f <sub> -v </sub> (S,T)* = $\Sigma$ <sub> u ∈ S' </sub> $\Sigma$ <sub> w ∈ T </sub> *f(u,w)* - $\Sigma$ <sub> w ∈ T  </sub> $\Sigma$ <sub> u ∈ S'</sub> *f(w,u)* por ejemplo la contribución en *f(S,T)* para las aristas no incidentes en v

#### Conservación del flujo en los cortes-(s,t)

**Teorema**

*Sea* $\eta$ = *(V,E,c,s,t)* y *f* un flujo de $\eta$ . Para cada corte-(s,t) *(S,T), f(S,T)* = |*f*|

*Demostración:*

Por inducción sobre |S|

- Si S = {s} entonces, por definición, *f(S,T) =* |*f*|

- Assumimos es cierto para *S' = S* - {*v*} y *T' = T* $\cup$ {*v*}, por ejemplo *f(S',T')* = |*f*|

- HI: *f(S',T')* = |*f*|

- Entonces, *f(S,T)* = *f<sub>-v</sub> (S,T)* + *f(v,T)* + *f(T,v)*

- Pero, *f(S',T')* = *f<sub>-v</sub> (S,T)* + *f(S',v)* - *f(b,S')* como *v* $\in$ *T'*

- Por conservación del flujo: *f (S', v)* + *f(T, v) = f(v, S')* + *f(v ,T)*

- Por lo que,  *f (S', v)* - *f(v, S') = f(v, T)* - *f(T ,v)*

- Entonces, *f(S,T) = f(S',T') =* |*f*|

****

### Grafos residuales

*Sea* $\eta$ = *(V,E,c,s,t)* conjuntamente con un flujo *f*. 

El grafo residual G<sub>f</sub> = (V, E<sub>f</sub>, c<sub>f</sub>) es un digrafo con pesos con el mismo conjunto de vértices y com aristas:

- Si c(u,v) - f(u,v) > 0 entonces (u,v) $\in$ E<sub>f</sub> y c<sub>f</sub> (u,v) = c(u,v) - f(u,v) > 0 (forward edges). "Lo que no he servido". 

- Si f(u,v) > 0 entonces (v,u) $\in$ E<sub>f</sub> y c<sub>f</sub> (v,u) = f(u,v) - f(u,v) > 0 (backward edges). "Lo que he servido girando las aristas".
- Notad que si c(u,v) = f(u,v) solo hay una arista de retroceso.
- c<sub>f</sub> es conocido como la capacidad residual.
- forward edges: aún queda capacidad para enviar más flujo por la arista. 
- backward edges: las unidades de flujo que pueden ser redirigidas a través de otros links. 

****

### Camino de aumento

*Sea* $\eta$ = *(V,E,c,s,t)* y *f* un flujo en $\eta$. 

- Un camino de aumento *P* es un camino simple *P* en G<sub>f</sub> de s a t. 

- *P* puede tener forward y backward edges.

- Para un camino de aumento *P* en  G<sub>f</sub>, el cuello de botella b(P) es un la mínima capacidad (residual) de las aristas en *P*. 


*Pseudocódigo:*


    Augment(P,f):
        b = bottleneck (P)
        foreach (u,v) ∈ P do:
            si(u,v) es forward edge then
                Increase f(u,v) en b
            else
                Decrease f(v,u) en b
        return f

**Lemma:**

Sea f' = Augment(P,f), entonces f' es un flujo en G. 

*Demostración:*

Debemos demostrar las dos propiedades de flujo:

1) Ley de la capacidad
    
    - Forward edges (u,v) $\in$ P, incrementamos f(u,v) en b, como b $\leq$ c(u,v) - f(u,v) entonces f'(u,v) + b $\leq$ c(u,v)
    
    - Backward edges (u,v) $\in$ P, decrementamos f(v,u) en b, como b $\leq$ f(v,u), f'(v,u) = f(u,v) - b $\geq$ 0

2) Ley de la conservación, $\forall$ v $\in$ P \ {s,t} sea u el predecesor de v en P y sea w su sucesor

    -  Como el camino es simple solo las alteraciones dado (u,v) y (v,w) pueden cambiar el flujo que pasa por v. Tenemos 4 casos: 
    
        i. (u,v) y (v,w) son backward edges, el flujo en (v,u) y (w,v) es decrementado en b. Como uno es entrante y el otro saliente, el balance total es 0. 
        
        ii. (u,v) y (v,w) son forward edges, el flujo en (u,v) y (v,w) es incrementado en b. Como uno es entrante y el otro saliente, el balance total es 0. 
        iii. (u, v) es forward i (v, w) es backward, el flujo en (u, v) es incrementado en b y el flujo en (w,v) es decrementado en b. Como los dos son entrantes, el balance total es 0.
        
        iv. (u, v) es backward y (v, w) es forward, el flujo en (v, w) es incrementado en b y el flujo en (v,u) es decrementado en b. Como los dos son salientes, el balance total es 0.


**Lemma:**

Sea f' = Augment(P,f), entonces |f'| > |f|. 

*Demostración:*

Sea P un camino de aumento en G<sub>f</sub>. La primera arista e $\in$ P sale de s, y como G no tiene aristas entrantes en s, e es una arista de retroceso. Además, P es simple ⇒ nunca vuelve a s. 
Entonces, el valor del flujo incrementa en la arista e aumenta en b unidades. 

****

### Teorema Max-Flow min-cut

*Demostración:*

Sea *f* \* un flujo con máximo valor, |*f* \*| = max <sub> f </sub> {| *f* |}

- Para cualquier corte-(s,t) (S,T), *f* \*(S,T) $\leq$ c(S,T)

- G<sub>f*</sub> no tiene camino de aumento. Si S<sub>s</sub> = {v $\in$ V | $\exists$ s -> v in G<sub>f*</sub>}, entonces (S<sub>s</sub>, V - {S<sub>s</sub>}) es un corte-(s,t).

- Para e = (u,v) $\in$ E con u $\in$ S<sub>s</sub> y v $\notin$ S<sub>s</sub>, (u,v) $\notin$ E(G<sub>f*</sub>, por tanto f*(u,v) = c(u,v))

- Entonces, c(S<sub>s</sub>, V − {S<sub>s</sub>}) = f* (S<sub>s</sub> , V − {S<sub>s</sub>}) = |f*|

- (S<sub>s</sub>, V − {S<sub>s</sub>}) es la capacidad mínima del corte (s,t) en G

****
### Algoritmo de Ford-Fulkerson

Objectivo: El flujo máximo a través de una red

*Pseudocódigo:*

    Ford-Fulkerson(G, s, t, c): 
        forall(u,v) ∈ E set f(u,v) = 0
        Gf = G
        while haya un camino (s,t) P en Gf do:
            f = Augment(P, Gf)
            Compute Gf 
        return f

**Teorema:**

El flujo devuelto por FF es el max-flow

#### Red con capacidades enteras

1. INVARIANTE:

*Lema:*

Sea $\eta$ = *(V,E,c,s,t)* donde c : *E* $\rightarrow$ $\mathbb{Z^+}$. En cada iteración de FF, los valores de flujo f(e) son enteros.

*Demostración:*

Por inducción:

- La proposición es cierta para el flujo inicial (todo son 0). 

- HI: La proposición es cierta después de j iteraciones. 

- En la iteración j + 1: como las capacidades residuales en G<sub>f</sub> son enteros, el cuello de botella (P,f) $\in$ $\mathbb{Z}$ para el camino de aumento encontrado en la iteración j + 1. 

- Como consecuencia, los valores del flujo aumentado son enteros. 

2. TEOREMA:

*Lema*: 

Sea $\eta$ = *(V,E,c,s,t)* donde c : *E* $\rightarrow$ $\mathbb{Z^+}$. Existe un max-flow f* tal que f*(e) es entero, para cualquier e $\in$ E.

*Demostración:*

Como el algoritmo termina, el teorema sigue por del lema invariante de la integralidad. 

3. TIEMPO DE EJECUCIÓN

*Lema:* 

Sea C la capacidad min cut (= valor de max. flow), FF termina después de encontrar al menos C caminos de aumento. 

*Demostración:*

El valor del flujo incrementa en $\geq$ 1 después de cada aumento.

El número de iteraciones es $\leq$ C. En cada iteración:

- Construyendo G<sub>f</sub>, con *E*(G<sub>f</sub>) $\leq$ 2m, tiene coste O(m).

- O(n+m) para encontrar el camino de aumento o decidir si existe. 

- Coste total O(C \* (n+m)) = O(C\*m)

- Es pseudopolinómico

### Maximum matching problem

Dado un grafo no dirigido G = (V,E) un subconjunto de aristas M ⊆ E es una asignación si cada nodo aparece como mucho en una arista en M (un nodo puede no aparecer). 

Dado un grafo G, encontrar la asignación con máxima cardinalidad.

Un grafo G = (V,E) es bipartido si hay una partición de V en L y R tal que L ∪ R = V y L ∩ R = ∅, de tal manera que cada e ∈ E conecta un vértice de L con un vértice en R.

Queremos resolver el problema de la máxima asignación en grafos bipartidos. 

De G = (L ∪ R, E) construímos $\eta$ = *(V',E',c',s',t')*

- Añadir vértices s y t: V' =  L ∪ R ∪ {s, t}
- Añadir aristas dirigidas s → L con capacidad 1. Añadir aristas dirigidas de R → t con capacidad 1.
- Dirigir las aristas E de L a R, y dar capacidad $\infty$
- E' = {s → L} ∪ E ∪ {R → t}

**Teorema**

Max flow en $\eta$ = Asignación máxima bipartida en G

*Demostración: Asignación como flujos*

Sea M una asignación en G con k-aristas, consideramos el flujo *f* que envía una unidad a lo largo de cada k camino, s → u → v → t, para (u,v) ∈ M.


