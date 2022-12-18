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
-

**Algunas propiedades de G<sub>f</sub> y G'<sub>f</sub>**

¿Cómo podemos encontrar (u,v) ∈ E<sub>f'</sub> pero (u,v) $\notin$ E<sub>f</sub>?
  - (u,v) es una forward edge saturada en *f* y no en *f'*. 
  - (u,v) es una backward edge en G<sub>f</sub> y f(u,v) = 0

En cualquier de los dos casos, el aumento debe modificar v a u de manera que (u,v) debe formar parte del camino de aumento.

**Lema:**

Si el algoritmo EK se ejecuta en $\eta$ = (V, E, c, s, t), para todos los vertices v $\noteq$ s, $\delta<sub>f</sub>(s,v) crece monótonamente con cada flujo de aumento$

*Demostración: por reducción al absurdo*

Sea *f* el primer flujo tal que para alguna u $\noteq$ s,

$\delta<sub>f'</sub>(s,u) < $\delta<sub>f</sub>(s,u)

Sea v el vértice con minímo $\delta<sub>f'</sub>(s,v) cuya distancia es disminuida.

- Sea P: s--->u → v el camino con longitud menor de s a v en G<sub>f'</sub>
- Entonces, $\delta<sub>f'</sub>(s,v) = $\delta<sub>f'</sub>(s,u) + 1 y $\delta<sub>f'</sub>(s,u) $\geq$ $\delta<sub>f</sub>(s,u)
- Si (u,v) ∈ E<sub>f</sub>, $\delta<sub>f</sub>(s,v) $\leq$ $\delta<sub>f'</sub>(s,u) + 1 = $\delta<sub>f'</sub>(s,v)
- Entonces, (u,v) $\notin$ E<sub>f</sub>,

