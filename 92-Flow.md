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

**Efectos de cambiar el peso:

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

- *f <sub> -v </sub> (S,T)* = $\Sigma$ <sub> u ∈ S' </sub> $\Sigma$ <sub> w ∈ T </sub> *f(u,w)* - $\Sigma$ <sub> w ∈ T  </sub> $\Sigma$ <sub> u ∈ S' *f(w,u)* por ejemplo la contribución en *f(S,T)* para las aristas no incidentes en v

#### Conservación del flujo en los cortes-(s,t)

**Teorema**

*Sea $\eta$ = *(V,E,c,s,t)* y *f* un flujo de $\eta$ . Para cada corte-(s,t) (S,T), f(S,T) = |f|*

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

