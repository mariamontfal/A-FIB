# Algoritmos para data streams: Streaming models, graph streams

### **Los datos:**

*Características:*

    - Los datos llegan como una secuencia de ítems. 
    - Algunas veces, continuadamente y a alta velocidad. 
    - No se pueden guardar todos en la memoria principal. 
    - No se puede volver a leer; o si se leen tienen coste. 
    - Abstraemos los datos a una característica en particular, el campo de interés será la etiqueta. 
    - Tenemos un conjunto de n etiquetas Σ y nuestra entrada es stream.
        s = x1, x2, x3, ..., xm donde cada xi ∈ Σ.
    - Se tiene que tener en cuenta que algunas veces no se sabe el tamaño de la entrada del stream.
    - El objetivo es computar una funcion stream, p.ej. la mediana, el número distinto de elementos, la secuencia más larga creciente. 
    

*Aplicaciones prácticas:*

    - Redes más rápidas, almacenamiento menos costoso de datos, resultados para ser procesados de inicio de sesión ubicuos para un total de datos masivos.
    - Monitorización de redes, planigicación de consultas, eficiencia de I/O ...
    
*Aplicaciones teóricas:*

    - Fácil para instanciar problemas pero díficiles de resolver. 
    - Generadores pseudo-random, aproximaciones, computación paralela...
    
### **Modelo clásico de streaming:**

*Propiedades:*

1. Los datos son accedidos secuencialmente
2. El procesamiento de datos se hace secuencialmente utilizando una memoria pequeña O(polylog n). 
3. Medidas de complejidad: número de pasos sobre los datos, tamaño de la memoria, tiempo de procesamiento por ítem. 

### **Modelo semi-streaming:**

*Propiedades:*

1. Normalmente para problemas de grafos.
2. Memoria que trabaja es de O(n*polylog n), para un grafo con n vértices.
3. Suficiente espacio para guardar los vértices, pero no las aristas. 

*Objetivos algorítmicos de los modelos stream:*

    - Los datos normalmente son sin límite de tamaño.
    - Como el total de memoria y computación es limitado, puede ser imposible dar respuestas exactas. 
    - Los algoritmos utilizan una aletorieddad para buscar una respuesta aproximada (con un alto nivel de confianza).
    

### **Streams que describen grafos:**

*Propiedades*

    - G no dirigido
    - n vértices
    - El stream describe las aristas de G
    - Asumimos que una arista aparece una única vez en el stream
    - Queremos mantener el DS que permita responder consultas sobre una propiedad del grafo
    - O(n*log n) de memoria es razonable al estar trabajando con un modelo semi-stream.
    
**Problema: Decidir si una entrada de un grafo en stream es conexo o no.** 

Algoritmo:

    - Mantener un bosque generadores de H del grafo visto. 
    - Respuesta a la consulta acorde a H. 
G conexo si y solo si admite un árbol generador. 

Utilizando un union find DS amortizado tenemos O(α(n)) por ítem.

**Problema: Encontrar el máximo emparejamiento en G, dado un stream** 

Algoritmo: mantiene un emparejamiento M. 

    procedure MMatching(int n, stream s, double t)
        M=∅
        while not s.end() do
            (u,v) = s.read() 
            if M ∪ (u,v) is a matching then
                M = M ∪ {(u,v)} 
        On query, report M

O(n*log n) espacio, O(1) tiempo por ítem para las operaciones.
M es un emparejamiento maximal cuando produce una estimación â de tamaño a para un emparejamiento máximo. 
â es una aproximación a a, porque almenos, un vértice de cada arista de M debe estar emparejado con una arista en el emparejamiento máximo. 

### **Sampling:**
    - Es una técnica generar para abordar conjuntos de datos masivos. 
***
    
**RESERVOIR SAMPLING:**

***

**Problema: Mantener una muestra uniforme x del stream s para un tamaño desconocido.**  

El elemento seleccionado debe ser uno de los leídos con probabilidad uniforme. 

Algoritmo:

    - inicialmente x = x1
    - viendo t-iésimo elemento, x = xt con probabilidad 1/t
    
O(log n) memoria (en bits), O(1) tiempo por ítem para las operaciones.

**Problema: Mantener una muestra uniforme x de tamaño k del stream s con un tamaño desconocido.**  

El elemento seleccionado debe ser uno de los leídos con probabilidad uniforme. 

Algoritmo:

    - inicialmente X = {x1,x2,...,xk}
    - viendo t-iésimo elemento, donde t>k, seleccionar xt para ser añadido con probabilidad k/t
    - si xt es seleccionado para ser añadido, seleccionar uniformemente un elemento aleatorio de X, eliminarlo y añadir xt.
    
O(k*log n) memoria (en bits), O(1) tiempo por ítem para las operaciones.


**Problema: Mantener una muestra uniforme de k ítems sobre los w ítems últimos.**  

Con este problema no funciona Reservoir Sampling. 
    
*¿Por qué?*

    - Supon un elemento que no pertene a los w últimos. 
    - Se necesita reemplazar con un elemento escogido de forma aleatoria de la ventana actual. 
    - Pero, no tenemos acceso a los datos pasados.
    - Una solución podría ser guardar la ventana w con coste en espacio O(w).
    
Algoritmo (k=1):
    
    Mantener una muestra de reserva para los primeros w ítems en s, pero
    Cada vez que el último elemento xi es seleccionado, escoger e indexar j ∈ [w] uniformemente en random, xi+j será reemplazado por xi. 
    Para t>w, cuando t=i+j, set x=xi+j (y escoger el siguiente reemplazo).
    
    
O(log n + log w) en espacio y O(1) tiempo por ítem. 
Proporciona una muestra uniforme. 
Para valores mayores de k, ejecutar k cadenas paralelas de la muestra. Con una altra probabilidad, para k altas, esas cadenas no intersectarán.

