# Unidad 1

## 🛠 Fase: Apply

### Actividad 03
Escribe un programa que compare el valor almacenado en la dirección de memoria 5 con el valor 10. Si el valor es menor que 10, guarda el valor 1 en la dirección 7. Si el valor es mayor o igual a 10, guarda el valor 0 en la dirección 7.

Primero voy a escirbir cómo creo que se haría y después voy a corregir las partes en las qué tuve errores y analizar por qué

~~~
@5
D=M  // En la posicicón 5 de la memoria se guarda D

@10
D= D-A   // Para comparar el valor con D

@MENOR  // Para que vaya a la dirección de la etiqueta si es menor
D;JLT   // Si D es menor que haga un salto

(MENOR)
@7      // A es 7
M=1     // 1 va a la posición 7

@MAYOR // Para que vaya a la dirección de la etiqueta si es mayor
D;JGE  // Si D es mayor o igual que haga un salto

(MAYOR)
@7       // A es 7
M = 0    //Guarda en la dirección 7 el número 0 cuando ocurre la condición
~~~

Al observar el programa que hice, me di cuenta de que me falta una instrucción que evite que se sigan ejecutando las demás líneas después de cumplir la condición de que el valor sea menor que 10. También parece que la etiqueta de mayor sobra y me hace falta una etiqueta para indicar el final del programa. Así quedaría la corrección.

~~~
(LOOP)  // Etiqueta
@5      // A es 5
D=M     // Se carga en D lo que está en la posición 5

@10     // A es 10
D=D-A   // Se guarda en D el resultado de la operación

@MENOR   
D;JLT	  // Si D es menor salta a la etiqueta, si no se continua ejeutando el código como si fuese mayor o igual

@7       // A es 7
M=0      // Se guarda en la posición 7 el 0
@LOOP    // Va a la primera etiqueta por lo que se repite el ciclo
0;JMP    // Vuelve a empezar el ciclo

(MENOR)   // Etiqueta a la que salta si es menor
@7      
M=1      // Pone 1 en la posición 7
@LOOP 
0;JMP     // Vuelve a empezar el ciclo

~~~

Aprendí algo nuevo y es que al comparar los valores cuando por ejemplo se va a hacer el salto que toma el valor de  D y mira si es menor que 0 (D < 0), se haría así normalmente pero como antes había puesto D = D-A en este caso se pone ese valor en donde está la D y al despejarlo quedaría (D < 10)

### Actividad 04 
Crea un programa que use un ciclo para sumar los números del 1 al 5 y guarde el resultado en la dirección de memoria 12.

Voy a realizar una hipótesis de cómo creo que se haría antes de probarlo.
~~~
@1
D = A
D = D + A

(STOP)
D; JET

@STOP
@12
D = M
~~~
Al tratar de realizar la actividad me di cuenta que no tengo muy claro cómo puedo crear un ciclo con números que cambien constantemente, lo que se me ocurrió hacer que se detenga cuando llegue a 15 que es el resultado de sumar los números del 1 al 5. Me falto algo muy importante que era el loop, di por hecho que continuaría automátiamente al no detenerse.

~~~
@1      // A es 1
D=A     // D es 1
@16     // A es 16
M=D     // En la posición 16 se guarda el número 1 que sería el contador

@0      // A es 0
D=A     // D es 0
@17     // A es 17
M=D     // En la posición 17 se guarda el 0 que sería la suma
(LOOP)  // Etiqueta del ciclo
@16     // A es 16
D=M     // D toma el valor que está en la posición 16 
@6      // A es 6
D=D-A   // Se resta 6 para comparar
@END
D;JGE    // Si i >= 6 salta a END para terminar

@17     // A es 17
D=M     // D toma el valor de la suma
@16     // A es 16
D=D+M   // D = suma + i
@17     // A es 17
M=D     // Guarda la nueva suma en la posición 17

@16     // A es 16
M=M+1   // Incrementa i en 1

@LOOP
0;JMP   // Va a donde está la etiqueta

(END)   //Etiqueta
@17     // A es 17
D=M     // D toma el valor de la suma
@12     // A es 12
M=D     // Guarda el resultado en la posición 12

(ENDLOOP) //Etiqueta
@ENDLOOP 
0;JMP   // Salto para terminar el programa

~~~

A la hora de consultar pensé en la lógica a la hora de programar en c# y quería encontrar una forma de hacer ciclos donde se usa una variable que cuenta y otra para ir sumando. Quise hacer algo parecido en ensamblador pero no hay ciclos de ese tipo por lo que use etiquetas y saltos para repetir. Guardé el contador y la suma en diferentes posiciones de memoria para no mezclar las cosas. Cada vez que i es menor que 6, le sumo ese valor a la suma y luego aumento i. Cuando i llega a 6, paro el ciclo y guardo el resultado en la dirección 12.



