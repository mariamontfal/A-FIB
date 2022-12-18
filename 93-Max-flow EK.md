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
  
  
  
