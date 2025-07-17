# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01
#### 1. Reporta tus observaciones para cada experimento en tu bitácora de aprendizaje.
##### Experimento 1
Ejecuta el programa en el simulador de la CPU Hack y observa cómo se comporta. ¿Qué sucede? ¿Qué valor se almacena en la dirección de memoria 16? ¿Por qué crees que es ese valor?
Al ejecutar el programa se obtiene diversos resultados para cada una de las variables, según los registros A es 3, D es 7 y PC es 7, es decir la línea del código que se va a ejecutar. En la dirección de la memoria 16 se guarda el valor de 3. Esto es porque le asignamos a A el valor de 16 y al escribir el código M es igual a una variable, la M se guardará la variable que le demos en el valor que haya tomado A. 

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
En la memoria en la posición número 16 se guarda el valor de 3, los demás valores son 0. Y los registros, de A, D y PC cambian cada vez que se realizan operaciones hasta que finalmente se tienen los resultados de A siendo 7, D siendo 3 y PC siendo 7.

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
---
### Actividad 02
#### Experimento 
Antes de ejecutar cada instrucción vas a predecir qué crees que va a suceder. Es muy importante que hagas esto, de esta manera tu mismo puedes saber si estás entendiendo el programa.

Esto es lo que creo que va a suceder y después voy a analizar lo que realmente pasó y que se obtuvo como resultado:

~~~
@SCREEN         // A es 16384
D=A             // D es 16384
@i              // A es 16 porque es una variable no asignada
M=D             // En la posición 16 se va a guardar D que es 16384
(READKEYBOARD)  // Etiqueta para leer el teclado
@KBD            // A es 24576
D=M             // D es el valor que está en la posición 24576
@KEYPRESSED     // Creo que es como una variable
D;JNE           // Si D diferente de 0 que haga un salto
@i              // A es 16
D=M             // D es el valor que está en la memoria en la posición 16, arriba era 16384
@SCREEN         // A es 16384 
D=D-A           // El valor de D que es 16384 menos A que es 16384 toma un nuevo valor y D es 0 
@READKEYBOARD   // Creo que es algo relacionado con el teclado
D;JLE           // Si D es <= 0 entonces que haga un salto de linea
@i              // A es 16
M=M-1           // En la posición 16 se guarda el valor de la memoria menos 1, es decir 16485 menos 1 '''
A=M             // A ahora es una posición menos
M=0             // M es 0
@READKEYBOARD   // No sé qué es, pienso que lee el teclado o que A lo hace
0;JMP           // Salta a la parte en la que se lee el teclado

(KEYPRESSED)    // Etiqueta cuando se presiona el teclado
@i              // Ahora creo que A podría ser la tecla que es presionada
D=M             // No sé si D sería 0 porque todavía no hemos guardado algo o si este relacionado con el código anterior
@KBD            // A es 24576
D=D-A           // El valor anterior de D que no se cuál es, diré que es i menos 24576 
@READKEYBOARD   // Lee el keyboard
D;JGE           // No sé qué es, a lo mejor está relacionado con 0;JMP
@16             // A es 16
A=M             // Se le asigna un nuevo valor a A teniendo en cuenta la memoria
M=-1            // A la memoria se el resta uno
@i              // A es una posición
M=M+1           // El valor de A es la posición de M mas 1
@READKEYBOARD   // No tengo claro que es
0;JMP           // Salta a A
~~~
Al analizar los resultados qué obtuve no le veo mucho sentido por lo que creo que me falta comprender por qué fallaron las hipótesis por lo que voy a observar los resultados línea por línea en la página.

~~~
@SCREEN         // A es 16384
D=A             // D es 16384
@i              // Al ponerlo en nand2tetris vi que aparece como @16, consultando entendí que como es una variable que no está definida la primera libre
M=D             // En la posición 16 se guarda el número 16384
(READKEYBOARD)
@KBD
D=M
@KEYPRESSED
D;JNE
@i
D=M
@SCREEN
D=D-A
@READKEYBOARD
D;JLE
@i
M=M-1
A=M
M=0
@READKEYBOARD
0;JMP

(KEYPRESSED)
@i
D=M
@KBD
D=D-A
@READKEYBOARD
D;JGE
@16
A=M
M=-1
@i
M=M+1
@READKEYBOARD
0;JMP
~~~
















