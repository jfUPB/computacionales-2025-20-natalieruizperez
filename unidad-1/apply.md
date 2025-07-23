# Unidad 1

## 🛠 Fase: Apply

### Actividad 03
Escribe un programa que compare el valor almacenado en la dirección de memoria 5 con el valor 10. Si el valor es menor que 10, guarda el valor 1 en la dirección 7. Si el valor es mayor o igual a 10, guarda el valor 0 en la dirección 7.

Primero voy a escirbir cómo creo que se haría y después voy a corregir las partes en las qué tuve errores y analizar por qué

~~~
@5
D=M  // D= M[5]

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




