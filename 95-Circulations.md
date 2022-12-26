## Circulations

En estos nuevos problemas de flujo introducimos el escenario consumidor/productor. 

Algunos nodos serán capaces de producir un cierto flujo mientras otros serán consumidores de flujo. 

La pregunta es, si es posible dirigir "todo" el flujo producido a los consumidores. Cuando es possible, la asignación de flujo se llama circulación. 

Una red con demandas $\eta$ es una tupla (V, E, c, d) donde c asigna una capacidad positiva a cada arista. y d es una función para asociar una demanda d(v) a v $\in$ V.

- Si d(v) > 0, v puede recibir d(v) unidades de flujo más de las que manda (v es un sumidero - t). 
- Si d(v) < 0, v puede enviar d(v) uniidades de flujo más de las que recibe, (v es una fuente - s). 
- Si d(v) = 0, v no es ni sumidero ni fuente. 
- Definir S para ser un conjunto de fuentes y T para ser un conjunto de sumideros. 

Dada una red $\eta$ = (V, E, c, d) una circulación es una asignación de flujo f: E → $\mathbb{R}^+$

1) Capacidad: para cada e $\in$ E, 0 $\leq$ f(e) $\leq$ c(e)
2) Conservación: para cada v $\in$ V, $\Sigma$ <sub> (u,v) $\in$ E </sub> f(u,v) − $\Sigma$ <sub> (v,z) $\in$ E </sub> f(v,z) = d(v)

Puede no existir circulación

*Descripción del problema de circulación:*

Dada una red $\eta$ = (V, E, c, d) con c > 0, obtener la circulación si existe.

**Condiciones para que exista circulación:**
1) $\Sigma$ <sub> v $\in$ V </sub> d(v) =  $\Sigma$ <sub> v $\in$ V </sub> ( $\Sigma$ <sub> (u,v) $\in$ E </sub> f(u,v) - $\Sigma$ <sub> (v,z) $\in$ E </sub> f(v,z)) 

Para e = (u,v) $\in$ E, f(e) aparece en la suma de las aristas a v y en la suma de las aristas que salen de u. Los dos términos se cancelan.

Entonces tenemos que si existe una circulación: $\Sigma$ <sub> v $\in$ V </sub> d(v) = 0

Recordemos que:
- S = {v $\in$ V | d(v) < 0} y
- T = {v $\in$ V | d(v) > 0}

Definimos D = - $\Sigma$ <sub> v $\in$ S </sub> d(v) = $\Sigma$ <sub> v $\in$ T </sub> d(v). 

D es el total de flujo extra que es transporta desde las fuentes hasta los sumideros. 

De $\eta$ = (V, E, c, d) definimos la red de flujo $\eta$' = (V', E', c', s, t):

- V' = V ∪ {s,t}, añadimos una fuente s y un sumidero t. 
- Para v $\in$ S (d(v) < 0), añadimos (s,v) con capacidad -d(v)
- Para v $\in$ T (d(v) > 0), añadimos (v,t) con capacidad d(v)
- Mantenemos E y, para e $\in$ E, c'(e) = c(e)
