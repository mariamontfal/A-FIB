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
  
Si f es una circulación en $\eta$:
- Una unidad de flujo circula: s → i → j → t → s
- f(i,j) = 1 significa que el cliente i pide el producto j
- f(s,i) es el número de productos que el cliente i pide
- f(j,t) es el número de clientes que piden el producto j
- f(t,s) es el número total de productos servidos

**Teorema:**

$\eta$ tiene una circulación si y solo si hay un camino factible para diseñar la encuesta. 

*Demostración:*
Si existe un camino factible:
- Si i pregunta sobre j entonces f(i,j) = 1
- f(s,i) = número de preguntas pregunntadas a i ($\geq$ c<sub>i</sub>)
- f(j,t) = número de clientes que han sido preguntados sobre j ($\geq$ d<sub>j</sub>)
- f(t,s) = número total de preguntas
- fácil de verificar que f es una circulación en $\eta$
Si existe un circulación entera en $\eta$:
- si f(i,j) = 1 entonces i pregunta sobre j
- las restricciones satisfacen la regla de la capacidad

*Coste del algoritmo:*
- $\eta$ tiene N = n + m + 2 vértices y E = n + m + nm aristas
- L = $\Sigma$ <sub> e </sub> l(e) $\leq$ nm
- Obtener $\eta$ y extraer la informaciónn de la circulación tiene coste O(nm)
- FF análisis, el coste de obtener la circulación O(L(N+M)) = O(n<sup>2</sup>m<sup>2</sup>)
- EK análisis, el coste de obtener la circulación O(NM(N+M)) = O((n+m) n<sup>2</sup> m<sup>2</sup>)
- El algoritmo tiene coste O(n<sup>2</sup> m<sup>2</sup>)

## Redondeo con restricciones

Consideramos una matriz A = (a<sub>ij</sub>) con dimennsiones n x n, donde cada a<sub>ij</sub> $\in$ $\mathbb{R}^+$ ∪ {0} y donde la suma de cada fila y columna de A es un entero. Queremos redondear cada valor de a<sub>ij</sub> en ⌊a<sub>ij</sub>⌋ o ⌈a<sub>ij</sub>⌉ sin modificar la suma de las filas/columnas. 

El problema consiste en dada unna matriz A, producir un algoritmo eficiente para determinar si es posible redondear A i, si es posible, producir la matriz redondeada. 

Demostrar la correctitud del algoritmo e indicar la complejidad. 

Notamos que: 
- Los elementos de A que son enteros no se deben modificar. 
- Sea r<sub>i</sub> = $\Sigma$<sub>j=1</sub><sup> n </sup> (a<sub>ij</sub> - ⌊a<sub>ij</sub>⌋) i c<sub>j</sub> = $\Sigma$<sub>j=1</sub><sup> n </sup> (a<sub>ij</sub> - ⌊a<sub>ij</sub>⌋)
- Si las filas y columnas de A suman un entero, entonces r<sub>i</sub> i c<sub>j</sub> son enteros. 
- Además $\Sigma$r<sub>i</sub> = $\Sigma$c<sub>j</sub>

Para resolver el problema haremos una reducción de este problema a uno de circulación. 
Una unidad de flujo la podemos interpretar como la parte decimal que se redondea a 1.

Construir una red con demandas $\eta$ = (V, E, c, d) donde:
- Vértices: V = {x<sub>i</sub>, y<sub>i</sub> | 1 $\leq$ i $\leq$ n}. Los vértices x representan las filas y los y las columnas. 
- Aristas: E = {x<sub>i</sub>, y<sub>j</sub> | 1 $\leq$ i,j $\leq$ n} i a<sub>ij</sub> $\notin$ $\mathbb{Z}$.
- Capacidades: c(x<sub>i</sub>, y<sub>j</sub>) = 1
- Demandas: d(x<sub>i</sub>) = -r<sub>i</sub>, 1 $\leq$ i $\leq$ n, i d(y<sub>j</sub>) = c<sub>j</sub>

$\eta$ tiene O(n) vértices i O(n<sup>2</sup>) aristas. 

Si existe un redondeo de A, $\eta$ tiene una circulación con valores enteros (0,1)
- Sea B un redondeo de A, definimos una nueva matriz D donde
  d<sub>ij</sub> = 1 si b<sub>ij</sub> > a<sub>ij</sub>
  d<sub>ij</sub> = 0 sino
- Como B es un redondeo $\Sigma$d<sub>ij</sub> = $\Sigma$r<sub>i</sub> y  $\Sigma$d<sub>ij</sub> = $\Sigma$c<sub>i</sub>
- Entonces, el flujo f(i,j) = d<sub>ij</sub> es una circulación en $\eta$

Si $\eta$ tiene una circulación con valores enteros (0,1), existe un redondeo de A. 
- Sea f una circulación en $\eta$
- Definimos la matriz B como
  b<sub>i,j</sub> = a<sub>ij</sub> si a<sub>ij</sub> $\in$ $\mathbb{Z}$
  b<sub>i,j</sub> = ⌈a<sub>ij</sub>⌉ si a<sub>ij</sub> $\notin$ $\mathbb{Z}$ y f(i,j) = 1
  b<sub>i,j</sub> = ⌊a<sub>ij</sub>⌋ sino
- Como f es una circulación: 
$\Sigma$<sub>j</sub>b<sub>ij</sub> = $\Sigma$<sub>j</sub>a<sub>ij</sub> y $\Sigma$<sub>i</sub>b<sub>ij</sub> = $\Sigma$<sub>i</sub>a<sub>ij</sub> 
- Entonces , B es un redondeo válido para A

La construcción de $\eta$ tiene una complejidad de O(n<sup>2</sup>)
FF funciona en O(D|E|) donde D es la suma de las demandas positivas, por ejemplo, D = $\Sigma$r<sub>i</sub> = O(n<sup>2</sup>) y como |E| = O(n<sup>2</sup>), el número total de pasos es O(n<sup>4</sup>)

## Segmentación de imagenes

- En las imágenes digitales, un pixel es el elemento más pequeño controlable en la imagen representada en una pantalla. 
- Las imagenes son representadas por un rasterizador gráfico de imagenes, una estructura de datos matricial de puntos representando una graella rectangular de pixels o puntos de color. 
- Las direcciones de los pixeles corresponden a sus coordenadas físicas. 
- Deseamos etiquetar cada pixel como pertenenciente al primer plannno o al fondo. 
- Los pixeles de imagen como una cuadrícula de puntos. 
- Definimos un grafo no dirigido G = (V,E) donde V = conjunto de pixeles en la imagen y E = pares de pixeles vecinnos (en la cuadrícula). 

Información:
- Para cada pixel i, a<sub>i</sub> $\geq$ 0 es la estimación de i de que este en primer plano y b<sub>i</sub> $\geq$ 0 es la estimación de que i esté en el fondo. 
- Para cada (i,j) de los pixeles vecinos, existe una penalización de separación p<sub>ij</sub> $\geq$ 0 para colocar uno en primer plano y otro en el fondo. 

*Objetivos:*
- Para i isolado, si a<sub>i</sub> > b<sub>i</sub> preferimos etiquetar i como primer plano (sino como fondo). 
- Si muchos vecinos de i son etiquetas como fondo, preferimos etiquetar i como fondo. Esto hace el etiquetado i más suave minimizando el total primer plano / fondo. 

Queremos una partición V en A (conjunto de pixeles de primer plano) y B (conjunto de pixeles de fondo), tal que queremos maximizar la función objetivo:

$\Sigma$<sub>i $\in$ A</sub>a<sub>i</sub> + $\Sigma$<sub>j $\in$ B</sub>b<sub>j</sub> - $\Sigma$<sub>{(i,j) $\in$ E, i $\in$ A, j $\in$ B </sub>p<sub>ij</sub>

La segmentación tiene parecido a un problema de corte pero:
- Es una maximización diferente a la de min-cut
- G es no dirigido
- No tiene vértices s ni t (pero los podemos añadir)
- Sea Q = $\Sigma$<sub>i $\in$ V</sub> (a<sub>i</sub> + b<sub>i</sub>) entonces:
$\Sigma$<sub>i $\in$ A</sub>a<sub>i</sub> + $\Sigma$<sub>j $\in$ B</sub>b<sub>j</sub> = Q - $\Sigma$<sub>i $\in$ A</sub>b<sub>i</sub> + $\Sigma$<sub>j $\in$ B</sub>a<sub>j</sub>
- Es equivalente a maximixar: $\Sigma$<sub>i $\in$ A</sub>b<sub>i</sub> + $\Sigma$<sub>j $\in$ B</sub>a<sub>j</sub> + $\Sigma$<sub>{(i,j) $\in$ E, i $\in$ A, j $\in$ B </sub>p<sub>ij</sub>

Transformamos G = (V, E) en $\eta$ = (V', E', c, s, t):
- Añadiendo un nodo s para representar el primer plano
- Añadiendo un nodo t para representar el fondo
- V' = V ∪ {s,t}
- Para cada (v,u) $\in$ E creamos aristas dirigidas antiparalelas (u,v) y (v,u) en E'
- Para cada pixel i creamos aristas dirigidas (s,i) y (i,t)
- E' = {(s,v) ∪ (v,t)}<sub>v$\in$ E</sub> ∪ {(u,v) ∪ (v,u)}<sub>(u,v)$\in$E</sub>

Para cada i $\in$ V, c(s,i) = a<sub>i</sub>, c(i,t) = b<sub>i</sub>
Para cada (i,j) $\in$ E, c(i,j) = c(j,i) = p<sub>ij</sub>

Un (s,t) - corte (A',B') corresponde a la partición de los pixeles en (A,B) para A = A'- {s} y B = B' - {t}
- Una arista (s,j) con j $\in$ B contribuye con a<sub>j</sub> en c(A', B')
- Una arista (i,t) donde i $\in$ A contribuye con b<sub>j</sub> en c(A',B')
- Una arista (i,j) donde i $\in$ A y j $\in$ B contribuyen con p<sub>ij</sub> en c(A',B')

Entonces, 

c(A',B') = $\Sigma$<sub>i $\in$ A</sub>b<sub>i</sub> + $\Sigma$<sub>j $\in$ B</sub>a<sub>j</sub> + $\Sigma$<sub>{(i,j) $\in$ E, i $\in$ A, j $\in$ B </sub>p<sub>ij</sub>

Queremos encontrar un corte con unn valor mínimo en la cantidad anterior, el cual es el equivalente al problema del corte mínimo en $\eta$

El coste del algoritmo está determinado por el coste de encontrar un corte mínimo en la red asociada, por ejemplo, como los dos vértices y las aristas son O(nm), el coste del algoritmo es O((nm)<sup>3</sup>)
