# Algoritmos de ordenación rápida

### **Algoritmos de ordenación:**

*Características*

1. Los algoritmos ordenaran un array A[n] de enteros no negativos en el rango de [0,r]
2. La complejidad del algoritmo dependerá de r y de n
3. Para algunos valores de r, los algoritmos pueden tener coste O(n) ó o(n*log n)
 

 
### **Counting Sort:** 

Considera todos los posibles valores de i ∈ [0, r].

Para cada uno de ellos, cuenta cuantos elementos en A son más pequeños o iguales a i.

Utiliza esta información para colocar los elementos en el lugar correcto

Estructuras: 
    1. Entrada: A[n] 
    2. Salida: B[n]
    3. Interna: C[r+1]  //para hacer el conteo

*Pseudocódigo*

    CountingSort(A,r)
        for i=0 to r do:
        //Inicialización del array contador a 0
            C[i] = 0
        for i=0 to n-1 do:
        //Por ejemplo, A[i]=7 -> C[7]++
            C[A[i]] = C[A[i]]+1
        for i=1 to r do:
        //Acumula en la posición iésima de C el total de número que
        //son más pequeños o iguales a i
            C[i]=C[i] + C[i-1]
        for i=n-1 downto 0 do:
            B[C[A[i]]] = A[i]
            C[A[i]] = C[A[i]]-1
    
Coste del algoritmo: O(n+r), si r = O(n), el tiempo es lineal

Counting sort es estable: los números con el mismo valor aparecen en la salida en el mismo orden que en la entrada. 


### **Radix Sort:** 

Dado un array A con n números, cada uno tiene d dígitos en base b.


*Pseudocódigo:*

    Radix LSD (A,d,b)
        for i=1 to d do:
            Utilizar un algoritmo estable para ordenar A acorde con el iésimo valor del dígito
            
Los valores a ordenar están en el ranfo [0, 2^d].

    
Coste del algoritmo: T(n,d,b) = Θ(d (n + b)) donde n = números, d = dígitos y b = base.

### **Bucket Sort:** 




*Pseudocódigo*

    
Coste del algoritmo: O(n)

