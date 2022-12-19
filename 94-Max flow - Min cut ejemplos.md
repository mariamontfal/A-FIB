### Matchings en grafos regulares

Un grafo bipartido G = (V, E) donde V = L ∪ R, es d-regular si todo vértice tiene grado d. 

Demuestra que todo grafo bipartido d-regular tiene un matching de tamaño |L|.
Siempre tiene un matching perfecto?

*Pista:* considerad la red de flujo correspondiente y analizar la capacidad del min cut. 

**Una solución:**

Si el grafo bipartido es bipartido y d-regular, *d*|*L*| = |*E*| y *d*|*M*| = |*E*|, por lo tanto |*L*| = |*R*|.
Como el grafo es bipartido, podemos utilizar la formulación de maximum matching como problema de flujo y analizar la capacidad de los cortes.

En la red de flujo conectamos *s* con todos los vértices de *L* y todos los vértices de *R* con *t*. 
Luego orientamos todas las aristas de *L* hacia *R*. Asignamos capacidad 1 a todas las aristas. 

Como *cut*({s}, V ∪ {t}) = |*L*|. Nos basta con demostrar que cualquier otro s,t-corte tiene capacidad $\geq$ |*L*|
- *cut*({*s*} ∪ *V*, {*t*}) = |*R*| = |*L*|
- *cut*({*s*} ∪ *L*, *R* ∪ {*t*}) = d|*L*| $\geq$ |*L*|

Falta analizar cortes que dividan *L* y *R*.

**s,t-cortes:**

Consideremos un s,t-corte ({*s*} ∪ *L*<sub>1</sub> ∪ *L*<sub>2</sub> ∪ *R*<sub>1</sub>, *L*<sub>3</sub> ∪ *R*<sub>2</sub> ∪ {*t*})

(*L*<sub>1</sub>, *L*<sub>2</sub>, *L*<sub>3</sub>) es una partición de *L* y 

(*R*<sub>1</sub>, *R*<sub>2</sub>) es una partición de *R*

si u ∈ *L*<sub>1</sub>, *N*(u) ⊆ *R*<sub>1</sub> y, si u ∈ *L*<sub>2</sub>, *N*(u) ∩ *R*<sub>2</sub> $\neq$ ∅

Como todos los vértices en *L*<sub>2</sub>, *R*<sub>1</sub> tienen al menos un vecino en *T* y *s* está conectado con todos los vértices de *L*<sub>3</sub>.

*cut(S,T)* =≥ |*L*<sub>3</sub>| + |*L*<sub>2</sub>| + |*R*<sub>1</sub>|

- Todos los vecinos de vértices en *L*<sub>1</sub> están en *R*<sub>1</sub>. 
- El grafo es d-regular, *d*|*R*<sub>1</sub>| $\geq$ *d*|*L*<sub>1</sub>|, y *d*|*R*<sub>1</sub>| $\geq$ *d*|*L*<sub>1</sub>|

*cut(S, T)* $\geq$ |*L*<sub>3</sub> | + |*L*<sub>2</sub> | + |*L*<sub>1</sub> | ≥ |*L*|

Siempre hay un matching de tamaño |*L*| en un grafo bipartido d-regular y como |*L*| = |*R*| este matching es perfecto.
