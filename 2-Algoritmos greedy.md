# Algoritmos voraces (greedy algorithms)

### **Algoritmos voraces:**

*Objetivo*
    
    Diseñados principalmente para resolver problemas de optimización de combinatoria. 
    
    Dada una entrada, queremos computar una solución óptima acorde con alguna función objetivo. 
    
    Las soluciones están formadas por una secuencia de elementos. 
    
    Un algoritmo greedy obtiene una solución óptima haciendo una secuencia de elecciones (sin backtracking).
    
    Algunas veces no se obtiene la mejor solución, pero si una solución rápida. 
    

*Características*

1. En cada paso se escoge la mejor solución (miope) en el momento para la correspondiente componente de la solución. Después se resuelve el subproblema generado. 
2. La elección dependerá de elecciones anteriores, pero no futuras. 
3. En cada paso, el problema se reduce. 
4. Nunca hace backtracking

Para que funcione la estrategia *greedy*, se debe cumplir:
    - Greedy choice property: podemos llegar al óptimo global seleccionando óptimos locales
    - Optimal substructure: después de hacer alguna decisión loca, debe ser el caso de que la solución óptima al problema contenga la solución parcial construida. 
    
### **Fractional Knapsack:** 


Seleccionar el ítem con mayor ratio valor/peso siempre dirige hacia la solución óptima del Fractional Knapsack problem. 

*Pseudocódigo*

    Ordenar los elementos en valor decreciente de v/w
    S = {}; Val = 0; i=0;
    mientras W>0 && i<n do
        si w[i]<=W entonces
            S = S ++{(i,1)}; W = W-w[i]; Val = Val + v[i]
        sino
            S = S ++{i,W/w[i]}; Val = Val + v[i]*W/w[i]; 
            W = 0;
        fi si
        ++i;
        Eliminar i de O
    fi while
    devolver S
    
Coste del algoritmo anterior: O(n*log n)

### **Scheduling:** 

Configuración general: Dado un conjunto de n tareas (con diferentes características) para ser procesas por un solo procesador, proporciona un horario (dónde y cuándo cada tarea va a ser ejecutada) para optimizar según algun criterio.

#### **Interval Scheduling:** ####

*Características*

1. Dado un conjunto de n tareas, para i ∈ [n], la tarea i tiene un tiempo de inicio si y un tiempo de finalización fi tal que si<fi.
    
2. Solo se puede procesar una tarea en un tiempo específico. 
    
3. Queremos encontrar el conjunto de tareas mutuamente compatible donde las actividades i y j son compatible si [sifi) ∩ (sjfj] = ∅ con la medida máxima.

*Pseudocódigo*

        Ordenar A en orden ascendiente de A.f
        S = {0}
        j = 0 {puntero a la última tarea de S}
        for i = 1 to i = n-1 do
            si A[i].s>=S[j].f entonces
                S = S ∪ {i}; j = i;
            fi si
        fi for
        return S
    
Coste O(n*log n)


Si sabemos los tiempos de inicio y finalización de la tarea en segundos durante un día (24 horas), puede ser implementado en tiempo O(n). Utilizando un algoritmo de ordenación de coste lineal (p.ej. bucket sort).

#### **Weighted activity selection:** ####

*Características*

1. Dado un conjunto de n tareas para ser procesadas por una sola máquina, donde cada actividad tiene tiempo de inicio si y tiempo de finalización fi, con si<fi y peso wi.
    
2. Queremos encontrar el conjunto de tareas mutuamente compatibles tales que Σwi para i∈S es el máximo de entre todos los conjuntos.

Esta versión se soluciona con programación dinámica


#### **Lateness minimization problem:** ####

*Características*

1. Tenemos un solo procesador y n tareas para ser procesadas.
    
2. Una vez una tarea empieza a ser procesada, continua hasta que el procesador la completa.

3. Procesar la tarea i tiene tiempo ti. Además, la tarea i tiene un tiempo de entrega di. 

4. El objetivo es programar todas las tareas (p.ej. determinar el tiempo al que comenzará a ser procesada cada tarea). 

5. Queremos minimizar, sobre todas las tareas, el tiempo máximo que el tiempo de finalización supera su tiempo de entrega.

*Pseudocódigo*

        Ordenar A en orden ascendiente de A.d
        S[0] = 0; t = A[0].t;
        L = max(0,t-A[0].d);
        for i = 1 to i = n-1 do
            S[i]=t;
            t = t + A[i].t,
            L = max (L, max(0,t-A[i].d))
        fi for
        return (S,L)
    
Coste O(n*log n)

### **Optimal prefix codes:**

#### **Huffman code:**

    - Dadas las frecuencias f(x) para cada x ∈ Σ
    - El algoritmo mantiene una lista dinámica ordenada en una cola de prioridad Q
    - Construir el tree bottom-up
        - Insertar los símbolos como hojas con clave f
        - Extraer los dos primeros elementos de Q y unirlos a un nuevo nodo virtual con la suma de las f´s de sus hijos como clave. Insertar el nuevo nodo en Q. 
    - Cuando Q tiene tamaño 1, el árbol resultante será el árbol de prefijos con un código de prefijos óptimo. 
    
*Pseudocódigo*
    
        Huffman (Σ, S)
        Dados Σ, S {computar las frecuencias {f}}
        Construir una cola de prioridad Q con las hojas para Σ, ordenar en orden creciente de f
        mientras Q.size()>1 do 
            crear un nuevo nodo z
            x = extraer-min(Q)
            y = extraer-min(Q)
            x e y hijos de z
            f(z) = f(x) + f(y)
        fi mientras
        φ = extraer-min(Q)
        
Si Q está implementada con un Heap, el algoritmo tarda O (n*log n)
    



    
