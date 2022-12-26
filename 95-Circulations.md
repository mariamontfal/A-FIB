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

Introducimos una nueva restricción l(e) para cada e $\in$ E, indicando el valor mínimo de flujo que debe haber en e. 

Una red $\eta$ com demandas y límites inferiores es una tupla (V, E, c, l, d) con c(e) $\geq$ l(e) $\geq$ 0, para cada e $\in$ E

Dada una red $\eta$ = (V, E, c, l, d) una circulación como una asignación de flujo f: E → $\mathbb{R}^+$
1) Capacidad: para cada e $\in$ E, l(e) $\leq$ f(e) $\leq$ c(e)
2) Conservación: para cada v $\in$ V, $\Sigma$ <sub> (u,v) $\in$ E </sub> f(u,v) - $\Sigma$ <sub> (v,z) $\in$ E </sub> f(v,z) = d(v)

Una circulación puede no existir. 

La circulación con demandas y límites inferiores: 

- Dado $\eta$ = (V, E, c, l, d), construimos una red $\eta$' = (V, E, c', d') con las demandas del siguiente modo:

Inicialmente seteamos c' = c y d' = d
Para cada e = (u,v) $\in$ E, con l(e) > 0:
  - c'(e) = c(e) - l(e)
  - Actualizamos las demandas en los dos extremos de e:
  d'(u) = d(u) + l(e) y d'(v) = d(v) - l(e)
  
1) Si f es una circulación en $\eta$, f'(e) = f(e) - l(e), para e $\in$ E, es una circulación en $\eta$'.

Por construcción de $\eta$', f' verifica la restricción de capacidad. 

A parte, para (u,v) con l(u,v) > 0, el flujo de salida de u y el flujo de entrada v es decreciente para l(u,v). 

f es una circulación en $\eta$ así que, el balance de flujo de f' coincide con la demanda d' de cada nodo. 

2) Si f' es una circulación en $\eta$', f(e) = f'(e) + l(e), para e $\in$ E, es una circulación en $\eta$.

f' verifica la restricción de capacidad f'(e) $\geq$ 0, así f'(e) $\geq$ l(e). 

f' es una circulación, el balance de f' en u es d'(u). 

Además, para (u,v) con l(u,v) > 0, el incremento de flujo en (u,v) balancea l(u,v) unidades de flujo de salida de u con l(u,v) unidades de flujo entrante en v. El balance en u es d(u).

### Main result

**Teorema:**

Existe una circulación en $\eta$ si y solo si existe una circulación en $\eta$'. Además, si todas las demandas, capacidades y límites inferiores en $\eta$ son enteros, y $\eta$ admite una circulación, hay una circulación en $\eta$ que tiene un valor entero. 

La parte circulación con valor entero es una consecuencia de la circulación con valor entero. Teorema para f' en G'. 

El coste del algoritmo es el mismo al coste del algortmo para circulación con demandas. 

**Teorema:**
Si todas las capacidades, límites inferiores y demandas son enteras y existe circulación, podemos obtener el valor de la circulación en tiempo O((D+L)m) donde L es la suma de los límites inferiores. 

## Ejemplos

## Survey Design problem

- Cliente i solo puede ser preguntado sobre comprar productos y debe recibir un cuestionario con almenos c<sub>i</sub> de esos productos, esos calores determinan la función de los productos comprados. 
- Para cada producto j, se quiere recolectar los datos de un mínimo de p<sub>j</sub> clientes. 

La entrada del problema es:

Un conjunto C de n clientes y un conjunto P con m productos.
- Para cada cliente i $\in$ C, una lista de productos comprados y dos valores c<sub>i</sub> $\leq$ c'<sub>i</sub>.
- Para cada producto j $\in$ P, dos valores p<sub>j</sub> y p'<sub>j</sub>.

Alternativamente, 

- La información sobre las compras debe ser representada como un grafo bipartido G = (C ∪ P, E), donde C es el conjunto de clientnes y P el conjunto de productos.
- (i,j) $\in$ E significa i $\in$ C compra el producto j $\in$ P

## Survey Design problem: circulación con límites inferiores

Construímos $\eta$ = (V', E', c, l) desde G según lo siguiente:

- Nodos: V' = V ∪ {s,t}
- Aristas: E' contiene E y aristas s → {C}, {P} → t, y (t,s)
- Capacidades y límites inferiores:
  - c(t,s) = $\infty$ y l(t,s) = 0
  - Para i $\in$ C, l(s,i) = c<sub>i</sub> y c(s,i) = el número de productos comprados. 
  - Para j $\in$ P, l(j,t) = p<sub>j</sub> y c(j,t) = número de clientes que compran j.
  - Para (i,j) $\in$ E, c(i,j) = 1 y l(i,j) = 0
