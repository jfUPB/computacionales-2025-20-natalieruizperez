# Unidad 1

## 🛠 Fase: Apply

### Actividad 03
Escribe un programa que compare el valor almacenado en la dirección de memoria 5 con el valor 10. Si el valor es menor que 10, guarda el valor 1 en la dirección 7. Si el valor es mayor o igual a 10, guarda el valor 0 en la dirección 7.

Primero voy a escirbir cómo creo que se haría y después voy a corregir las partes en las qué tuve errores y analizar por qué

~~~
@5
D=M  // En la posicicón 5 de la memoria se guarda D

@10
D= D-A

@MENOR  // Para que vaya a la dirección de la etiqueta si es menor
D;JLT

(MENOR)
@7
M=1

@MAYOR
D;JGE

(MAYOR)
@7
M = 0    //Guarda en la dirección 7 el número 0 cuando ocurre la condición
~~~

Al observar el programa que hice, me di cuenta de que me falta una instrucción que evite que se sigan ejecutando las demás líneas después de cumplir la condición de que el valor sea menor que 10. También parece que la etiqueta de mayor sobra y me hace falta una etiqueta para indicar el final del programa. Así quedaría la corrección.

~~~
(LOOP)
@5
D=M  // Se carga en D lo que está en la posición 5

@10
D=D-A   // Se guarda en D el resultado de la operación

@MENOR   // Si es menor salta a la etiqueta, si no se continua ejeutando el código como si fuese mayor o igual
D;JLT	

@7      
M=0      // Se guarda en la posición 7 el 0
@LOOP   // Va a la primera etiqueta por lo que se repite el ciclo
0;JMP

(MENOR)   //Etiqueta a la que salta si es menor
@7      
M=1      //Pone 1 en la posición 7
@LOOP
0;JMP

~~~

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
@1
D=A         // D es 1
@12
M=D         // Para guardar el resultado de 1 en la dirección 12

(LOOP)
@12
D=M          // Tomo el valor que está en esa dirección, o sea el 1
@2
D=D+A        // Daría 3 al sumarle el 2 al 1
@12
M=D          // Para guardar el valor que dio
@1
D=A          // D es 1 
@LOOP
D;JLT        // Si D < 5, saltamos al inicio del ciclo

(END)
@END
0;JMP        // Bucle infinito para terminar el programa

~~~



