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
    

