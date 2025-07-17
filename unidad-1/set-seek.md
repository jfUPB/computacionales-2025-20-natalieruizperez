# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01
#### 1. Reporta tus observaciones para cada experimento en tu bitácora de aprendizaje.

##### Experimento 1
Ejecuta el programa en el simulador de la CPU Hack y observa cómo se comporta. ¿Qué sucede? ¿Qué valor se almacena en la dirección de memoria 16? ¿Por qué crees que es ese valor? ¿Qué instrucciones se ejecutan en cada ciclo Fetch-Decode-Execute? ¿Qué cambios observas en el contenido de la memoria y los registros? ¿Qué instrucciones se ejecutan en cada ciclo Fetch-Decode-Execute?

##### Experimento 2
Escribe un programa en lenguaje ensablador que sume los números 5 y 10, y almacene el resultado en la dirección de memoria 20. Utiliza el simulador de la CPU Hack para ejecutar tu programa y verifica que el resultado es correcto.

Tuve en cuenta el primer experimento para guiarme entonces seguí un proceso muy similar. Primero le asigne a A el 5 y después dije que D era igual a A para que se guardara el valor de 5 en D. Luego cambié de nuevo el valor de A y dije que D = D + A para que se sumaran el 5 y el 10 y se guardara el valor en D.  Para finalizar dije que A era 20 para que el programa tuviese encuenta en qué posición quiero que se guarde el resultado y puse que M =

@5
D=A
@10
D=D+A
@20
M=D
@END
(END)
0;JMP

#### 2. ¿Qué diferencia hay entre los datos almancenados en la memoria ROM y en la RAM?
En la ROM es donde se guardan las instrucciones y por medio de la RAM es posible ejecutarlas.
