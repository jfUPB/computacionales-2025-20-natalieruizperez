# Unidad 2


## 🛠 Fase: Apply

### Actividad 06
Experimenta con arreglos

```
int arr[] = {1,2,3,4,5,6,7,8,9,10};
int sum = 0;

for (int j = 0; j < 10; j++) {
    sum = sum + arr[j];
}
```

**Implementa el programa anterior en lenguaje ensamblador aplicando el concepto de punteros y considera que los datos del arreglo están almacenados desde la dirección 16. Inicializa el arreglo en lenguaje ensamblador.**
Primero voy a analizar el programa, veo que tengo una lista de números del 1 al 10 y también una variable suma que inicia en 0 que sirve para acumular valores. Después veo que hay un ciclo que empieza en 0 y se repite varias veces hasta que la variable j es menor que 10. Cada vez que sucede el ciclo se toma el valor de la sum + el número que está en la posición j.

#### Prueba 01
Teniendo esto en cuenta voy a hacer la primera prueba para ver si funciona el código 

```
@0                   // A es 0
D=A                  // D es 0 que sería sum
@sum                   // Para guardar aquí la suma
M=D                  // La suma se guarda en la posición 16

//Hasta aquí creo que voy bien porque logicamente le veo sentido
//Voy a intentar hacer el ciclo

@1
D=D+A                // Ahora la suma debería ser 1
@sum
M=D                 // Aquí ya debería de sobrescribir la suma a la nueva

```
#### Prueba 02
Analizando el código que hice me di cuenta que en ninguna parte intenté crear j entonces haré a continuación otra hipótesis. La forma anterior es muy tediosa ya que tendría que hacer el ciclo con @2 y volver a copiar el último bloque, sería un código muy extenso.

```
@0                  // A es 0
D=A                 // D es 0
@sum                // Para guardar aquí la suma
M=D                 // En la posición i se guarda D que es 0

@0                  // A es 0
D=A                 // D es 0
@j                  // Aquí sería como para hacer un for en el que j empieza en 0
M=D                 // En la posición j se guarda el 0

```
#### Prueba 03
Aquí volví a intentar el código pero no recordaba bien como crear el puntero así que decidí devolverme a la actividad anterior y me sirvió para recordar conceptos y el cómo se traducía el puntero el lenguaje ensamblador.
```
// int *p;
// p = &a;
// Esta parte es la misma que la de arriba
@a
D=A          
@p
M=D      
```
#### Prueba 04
Teniendo en cuenta el código anterior crearé el puntero e intentaré usarlo.
```
@0                  // A es 0
D=A                 // D es 0
@sum                // Para guardar aquí la suma
M=D                 // En la posición i se guarda D que es 0

@0                  // A es 0
D=A                 // D es 0
@j                  // Aquí sería como para hacer un for en el que j empieza en 0 y luego para saber en que parte del ciclo va
M=D                 // En la posición j se guarda el 0

@16                // A es 16
D=A                // D es 16
@p                 // Dirección p
M=D                // p es 16 y estaría al principio del arreglo

@p
D=A                //D es p
@sum
M=M+D              // Al valor de sum le sumo el valor que está en p

```
#### Prueba 05
Hay un error y es que en lugar de estar haciendo lo que predije al final el programa está sumando sum + la dirección de p.

```
@0                  // A es 0
D=A                 // D es 0
@sum                // Para guardar aquí la suma
M=D                 // En la posición i se guarda D que es 0

@0                  // A es 0
D=A                 // D es 0
@j                  // Aquí sería como para hacer un for en el que j empieza en 0 y luego para saber en que parte del ciclo va
M=D                 // En la posición j se guarda el 0

@16                // A es 16
D=A                // D es 16
@p                 // Dirección p
M=D                // p es 16 y estaría al principio del arreglo

@p
A=M     // A es la dirección hacia donde apunta el p
D=M     // D es el valor en esa dirección
@sum
M=M+D    // A sum le sumo el valor que está en la dirección que apunta p

```
#### Prueba 06
Pensé que ahí ya estaría bien el código porque tengo forma de apuntar, sumar y llevar la cuenta pero me faltaba el ciclo que es algo fundamental. Necesito implementar el for pero en la activiad anterior se llegó a la conclusión de que no es posible crearlo de forma sencilla así que usaré una etiqueta.
```
@0                  // A es 0
D=A                 // D es 0
@sum                // Para guardar aquí la suma
M=D                 // En la posición i se guarda D que es 0

@0                  // A es 0
D=A                 // D es 0
@j                  // Aquí sería como para hacer un for en el que j empieza en 0 y luego para saber en que parte del ciclo va
M=D                 // En la posición j se guarda el 0

@16                // A es 16
D=A                // D es 16
@p                 // Dirección p
M=D                // p es 16 y estaría al principio del arreglo


(LOOP)      // Donde empeieza el ciclo, ya tengo creados el arreglo, puntero y suma
@p          // Lo mismo del código anterior pero poniéndolo en el ciclo porque quiero que se repita
A=M
D=M         
@sum
M=M+D      

@p
M=M+1      // p++

@j
M=M+1      // j++

@j
D=M
@10
D=D-A
@LOOP
D;JLT      // mientras j < 10, repetir
```

Construye tu programa PASO A PASO mediante pruebas. Indica qué característica vas a implementar con cada prueba y cómo la probaste.
Muestra el programa final y cómo lo probaste.








