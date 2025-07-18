# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01
#### 1. Reporta tus observaciones para cada experimento en tu bitácora de aprendizaje.
##### Experimento 1
##### Ejecuta el programa en el simulador de la CPU Hack y observa cómo se comporta. ¿Qué sucede? ¿Qué valor se almacena en la dirección de memoria 16? ¿Por qué crees que es ese valor?
Al ejecutar el programa se obtiene diversos resultados para cada una de las variables, según los registros A es 3, D es 7 y PC es 7, es decir la línea del código que se va a ejecutar. En la dirección de la memoria 16 se guarda el valor de 3. Esto es porque le asignamos a A el valor de 16 y al escribir el código M es igual a una variable, la M se guardará la variable que le demos en el valor que haya tomado A. 

#### ¿Qué instrucciones se ejecutan en cada ciclo Fetch-Decode-Execute?
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
#### ¿Qué cambios observas en el contenido de la memoria y los registros?
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

   ROM significa Read-Only-Memory, como su nombre lo indica en esta se almacena el programa o instrucciones, o sea del código que será ejecutado. En cambio, la RAM que significa Random Access Memory se usa para guardar y modificar datos mientras que se ejecuta el programa, como por ejemplo las variables o los resultados intermedios.

---
### Actividad 02
#### Experimento 
#### Antes de ejecutar cada instrucción vas a predecir qué crees que va a suceder. Es muy importante que hagas esto, de esta manera tu mismo puedes saber si estás entendiendo el programa.

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
@i              // A es 16
D=M             // D es el valor que está en la posición 16, es decir 16485
@KBD            // A es 24576
D=D-A           // 16485 - 24576
@READKEYBOARD   // Una etiqueta, no tengo muy claro que hace
D;JGE           // Si D es mayor o igual a 0 hace un salto
@16             // A es 16
A=M             // A es lo que está en la posición 16, es decir 16385
M=-1            // M es -1 
@i              // A es 16
M=M+1           // M es 0
@READKEYBOARD   // Una etiqueta
0;JMP           // Hace un salto 
~~~
Al analizar los resultados qué obtuve no le veo mucho sentido por lo que creo que me falta comprender, mi hipótesis falló por lo que voy a observar los resultados línea por línea en la página de nanotetris.

~~~
@SCREEN         // A es 16384
D=A             // D es 16384
@i              // A es 16 porque es una variable no asignada
M=D             // En la posición 16 se va a guardar D que es 16384
(READKEYBOARD)  // Etiqueta 
@KBD            // A es 24576
D=M             // D es el valor que está en la posición 24576
@KEYPRESSED     // Etiqueta a la que se va si se presiona una tecla
D;JNE           // Si D diferente de 0 que haga un salto a keypressed, lo que quiere decir que se está presionando una tecla
@i              // A es 16
D=M             // D es el valor que está en la memoria en la posición 16, arriba era 16384
@SCREEN         // A es 16384 
D=D-A           // El valor de D que es 16384 menos A que es 16384 toma un nuevo valor y D es 0 
@READKEYBOARD   // Instrucción de ir a esa etiqueta
D;JLE           // Si D es <= 0 entonces que haga un salto  a readykeyboard
@i              // A es 16
M=M-1           // En la posición 16 se guarda el valor de la memoria menos 1, es decir 16384 menos 1
A=M             // A ahora es 16483
M=0             // M es 0
@READKEYBOARD   // Instruccion de ir a esa etiqueta 
0;JMP           // Salta a el valor de a

(KEYPRESSED)    // Etiqueta
@i              // A es 16
D=M             // D es el valor que está en la posición 16, es decir 16384
@KBD            // A es 24576
D=D-A           // 16384 - 24576
@READKEYBOARD   // Instrucción de ir a la etiqueta
D;JGE           // Si D es mayor o igual a 0 hace un salto a donde estaba la etiqueta
@16             // A es 16
A=M             // A es lo que está en la posición 16, 16384
M=-1            // La posición 16384 es -1
@i              // A es 16
M=M+1           // M es 16384 + 1, es decir 16385
@READKEYBOARD   // Posición en la que está la etiqueta
0;JMP           // Hace un salto a la etiqueta
~~~

Después de observar me dicuenta que tenía problemas conceptuales, las etiquetas que pongo están entre paréntesis y mayúsculas las confundía con comentarios. Lo que tiene arroba y mayúsculas es para asignarle a A ese valor y al hacer el salta a la línea en la que puse la etiqueta. Adicionalmente me di cuenta que las etiquetas pueden tener el nombre que quiera. 

---
#### Bitácora
##### Identifica una instrucción que use la ALU y explica qué hace.
Una instrucción que usa la ALU sería D=D-A, porque hace una operación aritmética entre D y A. La ALU calcula el valor de D menos A y guarda el resultado en D.

##### ¿Para qué sirve el registro PC?
PC significa Program Counter y este se encarga de guardar la dirección de la siguiente instrucción que se va a ejecutar en el programa.

##### ¿Cuál es la diferencia entre @i y @READKEYBOARD?
@i es una variable que apunta a una dirección en RAM. En cambio, @READKEYBOARD es una etiqueta, que representa una dirección en la ROM donde hay una instrucción.
La diferencia entre @i y @READKEYBOARD es que el @i apunta hacia una dirección de la RAM. En cambio, el @READKEYBOARD le da a la A ese valor y después va a la dirección en la ROM en donde se dejó la etiqueta.

##### Describe qué se necesita para leer el teclado y mostrar información en la pantalla.
Para leer el teclado se necesita poner @KBD que es 24576, si no se presiona una tecla el valor es 0, en cambio si es presionada toma un valor. Para mostrar información en pantalla, se escribe un valor en la memoria a partir de @SCREEN que es 16384, donde cada posición representa un fragmento de la pantalla. 

##### Identifica un bucle en el programa y explica su funcionamiento.
Un bucle en el programa sería (READKEYBOARD) que ocurre si no se está apretando ninguna tecla, en el caso de ser presionada se interrumpe el bucle y va a (KEYPRESSED). Estos sirven para que el programa siempre corra, a menos que aparezca una condición que lo interrumpa.

##### Identifica una condición en el programa y explica su funcionamiento.
Una condición en el programa sería por ejemplo D;JNE, lo que esto hace es que realiza un salto si D es diferente de 0. Los condicionales sirven para que el programa pueda tomar decisiones y ejecutar diferentes acciones según lo que esté ocurriendo, debido a esto, el programa no siempre hace lo mismo, sino que puede adaptarse si se cumple una condición específica. 













