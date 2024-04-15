Las estructuras secuenciales son aquellas en las que las acciones se ejecutan una a continuación de la otra, en secuencia, no se bifurca ni se repite el flujo del programa. Por ejemplo: 

```
leer(A) 
leer(B) 
suma <-- A + B 
mostrar(suma)
```

Las acciones anteriormente indicadas se ejecutan cuando la anterior ha finalizado. Es decir, la acción **leer(B)** se ejecutará luego de que finalice la acción **leer(A)**, la acción **suma <-- A + B** se ejecutará una vez finalizada la acción **leer(B)**, y así sucesivamente