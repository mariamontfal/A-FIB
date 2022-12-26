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

### Problema de circulación: reducción a Max-flow

1) Cada flujo f' en $\eta$' verifica que |f'| $\leq$ D

La capacidad c'({s}, V) = D, por la restricción de capacidad en el flujo, |f'| $\leq$ D

2) Si hay una circulación f en $\eta$, tenemos un flujo máximo f' en $\eta$' con |f'| = D

Extendemos f a un flujo f', asignando f'(s,v) = -d(v), para v $\in$ S, y f'(u,t) = d(u) para u $\in$ T

Por la condición de circulación, f' es un flujo en $\eta$'. Además, |f'| = D.

3) Si hay un flujo f' en $\eta$' con |f'| = D, $\eta$ tiene una circulación. 

Para e $\in$ E, definimos f(e) = f'(e)

- Como |f'| = D, todas las aristas (s,v) $\in$ E' y (u,t) $\in$ E' estan saturadas por f'
- Por la conservación de flujo, f satisface d(v) = $\Sigma$ <sub> (u,v) $\in$ E </sub> f(u,v) - $\Sigma$ <sub> (v,z) $\in$ E </sub> f(v,z)
- Entonces, f es una circulación en $\eta$

De la discusión anterior podemos concluir:

**Teorema (condición necesaria y suficiente):**

Hay una circulación para $\eta$ = (V, E, c, d) si y solo si el flujo máximo en $\eta$' tiene valor D. 

**Teorema (Integralidad de circulación):**

Si todas las capacidades y demandas son enteras, y existe una circulación, existe un valor entero para el valor de la circulación. 

Demostración: formulación max-flow + teorema de integralidad para max-flow. 

**Teorema:**

Existe un algoritmo de tiempo polinómico para resolver el problema de circulación. 

El coste del algoritmo es el mismo que el coste del algoritmo utilizado para computar el flujo máximo. 

**Teorema:**

Si todas las capacidades y demandas son enteras, y existe una circulación, podemos obtener el valor enterio de la circulación en tiempo O(Dm)

## Redes con demanas y limítes inferiores

Generalización del problema anterior: además de satisfacer las demandas de los nodos, queremos forzar que el flujo utilice ciertas aristas. 
