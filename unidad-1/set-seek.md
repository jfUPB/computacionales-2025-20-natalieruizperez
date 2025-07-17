# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01
#### 1. Reporta tus observaciones para cada experimento en tu bitácora de aprendizaje.
##### Experimento 1
Ejecuta el programa en el simulador de la CPU Hack y observa cómo se comporta. ¿Qué sucede? ¿Qué valor se almacena en la dirección de memoria 16? ¿Por qué crees que es ese valor?
Al ejecutar el programa se obtiene diversos resultados para cada una de las variables. En la dirección de la memoria 16 se guarda el valor de 3. Esto es porque le asignamos a A el valor de 16 y al escribir el código M es igual a una variable, la M se guardará la variable que le demos en el valor que haya tomado A. 

¿Qué instrucciones se ejecutan en cada ciclo Fetch-Decode-Execute?
~~~
@1    // A es 1
D=A   // D es 1
@2    // A es 2
D=D+A // Como D es 1 y A es 2, la sumatoria es 3 y se guarda en D
@16   // A es 16
M=D   // La memoria guarda el resultado de D que es 3 en el valor que tiene A, es decir en la posición 16
@END  // A es END
(END) // Etiqueta
0;JMP // Salta al valor de A, es decir a END
~~~
¿Qué cambios observas en el contenido de la memoria y los registros?

---
##### Experimento 2
Escribe un programa en lenguaje ensablador que sume los números 5 y 10, y almacene el resultado en la dirección de memoria 20. Utiliza el simulador de la CPU Hack para ejecutar tu programa y verifica que el resultado es correcto.

~~~
@5    // Le asigno a A el 5
D=A   // D sería 5
@10   // Le asigno a A el 10
D=D+A // Al sumar A que es 10 y D que es 5 obtengo que la nueva D es 15
@20   // Le asigno a A el 20
M=D   // Ahora la memoria guarda a D en la posición que tenga a A como valor
@END  // A es END
(END) // Etiqueta
0;JMP // Salta al valor de A, es decir a END
~~~
---
#### 2. ¿Qué diferencia hay entre los datos almancenados en la memoria ROM y en la RAM?
En la ROM es donde se guardan las instrucciones y por medio de la RAM es posible ejecutarlas.
