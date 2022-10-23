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

#### **Weighted activity selection:** ####

#### **Minimizing lateness:** ####


    
