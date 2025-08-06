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

**Implementa el programa anterior en lenguaje ensamblador aplicando el concepto de punteros.**
Primero voy a analizar el programa, veo que tengo una lista de números del 1 al 10 y también una variable suma que inicia en 0 que sirve para acumular valores. Después veo que hay un ciclo que empieza en 0 y se repite varias veces hasta que la variable j es menor que 10. Cada vez que sucede el ciclo se toma el valor de la sum + el número que está en la posición j.

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

@1
D=A
@sum
M=M+D 

```
Me di cuenta que este código tiene un error después de que pongo el puntero porque estoy volviendo a hacer la suma manualmente y no uso el arreglo que cree.




Considera que los datos del arreglo están almacenados desde la dirección 16. Inicializa el arreglo en lenguaje ensamblador.
Simula paso a paso el programa en ensamblador. Recuerda la metodología: predice, ejecuta, observa y reflexiona.
Construye tu programa PASO A PASO mediante pruebas. Indica qué característica vas a implementar con cada prueba y cómo la probaste.
Muestra el programa final y cómo lo probaste.





