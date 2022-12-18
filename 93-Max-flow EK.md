### Edmonds Karg algorithm

Escoger un buen camino de aumento guía para un algoritmo más rápido. 

Aplica el algoritmo FF pero utilizando un BFS: escoge un camino de aumento en G<sub>f</sub> con la longitud más pequeña (número de aristas). 

*Pseudocódigo:*

  Edmods-Karp(G, c, s, t):
    para todo e = (u,v) ∈ *E* set *f*(u,v) = 0
    Gf = G
    mientras exista s---->t camino en Gf do:
      *P* = BFS(Gf, s, t)
      *f* = Augment(*f*, *P*)
      Computar Gf
    devolver *f*

Para $\eta$ = (V, E, c, s, t) y un flujo *f* en $\eta$, asumimos Gf tiene un camino de aumento, seteamos *f'* como el siguiente flujo después de ejecutar un paso del algoritmo EK.

- El camimo de s a t en un BFS empezando en s, es un camino s--->t con mínimo número de aristas. 
- Para v ∈ V, $\delta$ <sub>f</sub>(s,v) denota la longitud del camino mínimo de s a v en G<sub>f</sub>

**Algunas propiedades de G<sub>f</sub> y G'<sub>f</sub>**

¿Cómo podemos encontrar (u,v) ∈ E<sub>f'</sub> pero (u,v) $\notin$ E<sub>f</sub>?
  - (u,v) es una forward edge saturada en *f* y no en *f'*. 
  - (u,v) es una backward edge en G<sub>f</sub> y f(u,v) = 0

En cualquier de los dos casos, el aumento debe modificar v a u de manera que (u,v) debe formar parte del camino de aumento.

**Lema:**

Si el algoritmo EK se ejecuta en $\eta$ = (V, E, c, s, t), para todos los vertices v $\neq$ s, $\delta$<sub>f</sub>(s,v) crece monótonamente con cada flujo de aumento

*Demostración: por reducción al absurdo*

Sea *f* el primer flujo tal que para alguna u $\neq$ s,

$\delta$<sub>f'</sub>(s,u) < $\delta<sub>f</sub>(s,u)

Sea v el vértice con minímo $\delta$<sub>f'</sub>(s,v) cuya distancia es disminuida.

- Sea P: s--->u → v el camino con longitud menor de s a v en G<sub>f'</sub>
- Entonces, $\delta$<sub>f'</sub>(s,v) = $\delta$<sub>f'</sub>(s,u) + 1 y $\delta$<sub>f'</sub>(s,u) $\geq$ $\delta$<sub>f</sub>(s,u)
- Si (u,v) ∈ E<sub>f</sub>, $\delta$<sub>f</sub>(s,v) $\leq$ $\delta$<sub>f'</sub>(s,u) + 1 = $\delta$<sub>f'</sub>(s,v)
- Entonces, (u,v) $\notin$ E<sub>f</sub>,

¿Cómo podemos obtener?

- (u,v) \in E<sub>f'</sub> pero (u,v) \notin E<sub>f</sub>
- Si pasa, (v,u) aparece en el camino de aumento
- Entonces, el caminno con longitud mínima de s a u en G<sub>f</sub> tiene (v,u) como último vértice.

$\delta$<sub>f</sub> (s, v) ≤ $\delta$<sub>f</sub> (s, u) − 1 ≤ $\delta$<sub>f'</sub> (s, u) − 1 = $\delta$<sub>f'</sub> (s, v) − 1 − 1

Lo que contradice $\delta$<sub>f'</sub> (s,v) < $\delta$<sub>f</sub> (u,v)

**Alguna propiedades de G<sub>f</sub> y G<sub>f'</sub>**

Sea *P* un camino de aumento en G<sub>f</sub>. 
(u,v) \in *P* es crítico si b(*P*) = c<sub>f</sub>(u,v).

Las aristias críticas no aparecen en G<sub>f'<sub>
  - (u,v) forward, f'(u,v) = c(u,v)
  - (u,v) backward, f'(v,u) = 0
  
**Lema:**
  
  En el algoritmo EK, cada arista puede connvertirse en crítica como mucho |V| / 2 veces. 
  
*Demostración:*

- Sea (u,v) \in E, cuando (u,v) es crítico por primera vez, $\delta$<sub>f</sub> (s,v) =  $\delta$<sub>f</sub> (s,u) + 1
- Después de este paso, (u,v) desaparede del grafo residual hasta que el flujo en (u,v) cambie. 
  - En este punnto, (v,u) forman parte del camino de aumento en G<sub>f'</sub> y and $\delta$<sub>f'</sub> (s, u) = $\delta$<sub>f'</sub> (s, v) + 1,
$\delta$<sub>f'</sub> (s, u) = $\delta$<sub>f'</sub> (s, v) + 1 ≥ $\delta$<sub>f</sub> (s, v) + 1 ≥ $\delta$<sub>f</sub> (s, u) + 2
- Por lo que la distancia incrementa como mí
$\delta$<sub>f'</sub> (s, u) = $\delta$<sub>f'</sub> (s, v) + 1 ≥ $\delta$<sub>f</sub> (s, v) + 1 ≥ $\delta$<sub>f</sub> (s, u) + mí
$\delta$<sub>f'</sub> (s, u) = $\delta$<sub>f'</sub> (s, v) + 1 ≥ $\delta$<sub>f</sub> (s, v) + 1 ≥ $\delta$<sub>f</sub> (s, u) + mínimo en 2
  
**Teorema:**
El algoritmo de EK se ejecuta en O(mn(n+m)) pasos. Por lo que es un algoritmo polinómico. 
  - Necesita O(m+n) para encontrar el camino de aumento con un BFS.
  - Y por el lema anterior, hay O(mn) aumentos. 
  
#### Encontrando un corte mínimo

Dado (G, s, t, c) para encontrar un corte mínimo:
  1) Computar el flujo máximo f* en G
  2) Obtener G<sub>f*</sub>
  3) Encontrar el conjunto S = {v \in V | s---->v} en G<sub>f*</sub>
  4) Devolver el corte (S, V-{S}) = {(v,u) | v \in S and u \in V - {S}} en G. 
  
 El tiempo de ejecución es el mismo que el de encontrar el flujo máximo. 
  
El flujo máximo se puede computar en O(nm): J.Orlin (2013)
  
### Aplicaciones: problemas de asignaciones generalizadas
  
- Consideramos un problema de asignación generalizada GP donde, tenemos como input d conjuntos finitos X<sub>1</sub>, ..., X<sub>d</sub>, cada uno representando un conjunto diferente de recursos. 
- Nuestro objectivo es escoger el número de d-tuplas "más grande", cada d-tupla conteniendo exactamente un elemento para cada X<sub>i</sub>, sujeto a las siguientes restricciones:
  1) Para cada i ∈ [d], cada x ∈ X<sub>i</sub> puede aparecer en como mucho c(x) tuplas seleccionadas.
  2) Para cada i ∈ [d], cualquiera de las dos x ∈ X<sub>i</sub> e y ∈ X<sub>i+1</sub> puede aparecer como mucho c(x,y) tuplas seleccionadas. 
  3) Los valores para c(x) y c(x,y) estan en $\mathbb Z^+$ or $\infty$
- Notad que solo los pares de objetos adyacentes entre X<sub>i</sub> y X<sub>i+1</sub> estan restringidos.

Hacemos la reducción de GP a la siguiente red $\eta$:
- V contiene un vértice x, para cada elemento x en cada X<sub>i</sub>, y una copia x' para cada elemento x ∈ X<sub>i</sub> para 1 $\leq$ i < d
- Añadimos un vértice s y un vértice t
- Añadimos una arista s → x para cada x ∈ X<sub>1</sub> y añadimos una arista y → t para cada y ∈ X<sub>d</sub>. Dar capacidades c(s,x) = c(x) y c(y,t) = c(y). 
- Añadir una arista x' → y para cada par x ∈ X<sub>i</sub> e y ∈ X<sub>i+1</sub>. Dar una capacidad c(x,y). Omitir las aristas con capacidades 0.  
- Para cada x ∈ X<sub>i</sub> de 1 $\leq$ i < d, añadir una arista x → x' con capacidad c(x, x') = c(x).

Cada camino s---->t en $\eta$ identifica una posible d-tupla, sin embargo, cada d-tupla determina un camino s---->t.

- Para resolver GP, construimos $\eta$, y después encontramos un flujo máximo f* entero. 
- En el subgrafo formado por arista con f*(e)>0, encontramos un camino (s,t) *P* (una d-tupla), decrementamos en 1 el flujo en cada arista de *P*, eliminando aristas con flujo 0. 
- Repetimos el procedimiento para |f*| veces. En el camino obtemos un conjunto de d-tuplas con tamaño máximo verificando todas las restriccionnes.

#### Problema: Final's scheduling

- n cursos, cada uno con un final. Cada examen debe ser dado en una habitación. Cada curso c<sub>i</sub> tiene E[i] estudiantes. 
- r habitaciones. Cada r<sub>j</sub> tiene capacidad S[j]. 
- $\tau$ unidades de tiempo. Para cada habitación y unidad de tiempo, solo podemos asignar un final. 
- p profesores para vigilar exámenes. Cada examen necesita un profesor en cada clase y tiempo. Cada profesor tiene sus restricciones y disponibilidades y ningún profesor puede vigilar más de 6 finales. Para cada p<sub>l</sub> y $\tau$<sub>k</sub> definir una variable booleana A[k,l] = T si p<sub>l</sub> es disponible en $\tau$<sub>k</sub>.

Diseñar un algoritmo eficiente que programa correctamente una habitación, un rango de tiempo y un profesor para cada final, o reporta que no hay asignación posible. 

**Construcción de la red:**

Construimos una red $\eta$ con vértices {s, t, {c<sub>i</sub>}, {r<sub>j</sub>}, {$\tau$<sub>k</sub>}, {p<sub>l</sub>}}. Aristas y capacidades:
- (s, c<sub>i</sub>) con capacidad 1 (cada curso tiene un final)
- (c<sub>i</sub>, r<sub>j</sub>), si E[i] $\leq$ S[j] con capacidad $\infty$
- $\forall$ j, k (r<sub>j</sub>, $\tau$<sub>k</sub>), con capacidad 1 (un final por habitación y tiempo)
- ($\tau$<sub>k</sub>, p<sub>l</sub>), si A[k,l] = T, capacidad 1 (p puede vigilar un examen si p esta disponible en $\tau<sub>k</sub>$)
- (p<sub>l</sub>, t), capacidad 6 (cada p puede vigilar 6 o menos finales)

Nótese que ni las habitaciones ni los tiempos tienen restricciones individuales.

- El tamaño de la entrada es: N = n + r + $\tau$ + p + 2 y el tamaño de la red es O(N) vértices y O(N<sup>2</sup>) aristas. 
- Cada camino s---->t es una asignación de habitación-tiempo-profesor al final.
- Cada flujo entero identifica una colección de |*f*| (s, t)-caminos guiando a una asignación valido para |*f*| finales y viceversa. 
- Para maximizar el tiempo de finales dados, computamos el flujo máximo *f* * de s a t. 
- Si |*f* *| = n, entonces podemos programar todos los finales, sino no. 
- Para recuperar la asignación tenemos que considerar las aristas con flujo positivo y extraer la asignación de los n (s,t)-caminos. 
- Complejidad: 
  1) Construir $\eta$, tiempo O(N<sup>2</sup>)
  2) Como |*f* *| $\leq$ n enteros, podemos utilizar Ford-Fulkerson para computar *f* * con coste O(nN<sup>2</sup>)
  3) La segunda parte requiere O(N<sup>2</sup>). 
  4) El coste del algoritmo es: O(nN<sup>2</sup>) = O(n(n + r + $\tau$ + p)<sup>2</sup>)
