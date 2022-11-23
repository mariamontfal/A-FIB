# Shortest paths in digraphs

## Distances and shortest paths

Dado un digrapfo G = (V,E) con aristas con peso w: E → R

*Camino:*

- Un camino es una secuencia de vertices p = (v0,...,vk) la cual (vi,vi+1) ∈ E, para 0 ≤ i < k. 

- Un camino p = (v0,...,vk) tiene longitud l(p) = k y peso w(p) = Σ de i=0 a i = k-1 de w(vi, vi+1).

- Para un camino p = {u,...,v}, escribimismo u ->(p) v para decir que empieza en u y acaba en v. 

- Un camino permite vértices repetidos.

#### *Definiciones*

*Distancia:*

- Queremos asociar un valor para la distancia δ(u,v) para cada pareja de pares u, v en un digrafo con pesos (G,w), calculando el peso mínimo entre todos los caminos de u a v.

- Tenemos dos casos:
    
    1. Que no haya camino entre u y v, por lo que δ(u,v) = +∞.
    2. Que haya caminno entre u y v, por lo que la distancia será el min{w(p) | u->(p) v}. 

De otro modo, la distancia no puede ser definida. 

- **Teorema:** La distancia entre todos los pares u, v ∈ V (G) puede ser definida si y solo si, G no tiene ningún ciclo con peso negativo. En este caso, podrían definirse algunas distancias entre algunos pares, pero no todas. 

- Si G es no dirigido, consideramos cada arista en los dos sentidos y asignamos el mismo peso en ambas direcciones. 

- Si G no tiene pesos, podemos asignar a cada atista peso = 1. 

