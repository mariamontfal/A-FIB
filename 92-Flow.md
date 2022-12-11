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
