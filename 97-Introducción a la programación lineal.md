## Introducción a la programación lineal

En un problemma de programación lineal nos dan un conjunto de variables, una función objetivo, un conjunto de restricciones lineales y queremos asignar varoles reales a las variables de manera que:
- Se satisfacen el conjunto de ecuaciones lineales
- Se maximiza o minimiza la función objetivo

LP es de especial interés porque muchos problemas de optimización de combinatoria se pueden reducir a LP. 
Algunos ejemplos son: Max-Flow, problemas de asignación, matchings, caminos mínimos, MinST, etc. 

En un problema de programación lineal, el óptimo se consigue en un vértice de la región factible. 
Un problema de LP no es factible si:
- Las restricciones son tan restrictivas que es imposible satisfacerlas. 
- Las restricciones son tan poco restrictivas que la región no está limitada. 

### Forma estándar de un problema de programación lineal

1) Input:
Dado un conjunto de reales $(c_i)_{i=1}^{n}$, $(a_{ji})_{1 ≤ j ≤ m&1 ≤ i ≤ n}$ $(b_i)_{i=1}^n$
2) Output: valores reales para $\(x_i)_{i=1}^n$

Un problema de LP tiene forma estándar si:
- Restricciones no negativas para todas las variables. 
- Todas las restricciones son expresadas en forma de igualdad
- $\forall$ $b_i \geq$ 0 
