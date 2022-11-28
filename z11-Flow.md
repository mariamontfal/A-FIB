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
