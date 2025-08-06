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
@i                   // Para guardar aquí la suma
M=D                  // La suma se guarda en la posición 16

//Hasta aquí creo que voy bien porque logicamente le veo sentido
//Voy a intentar hacer el ciclo

@1
D=D+A                // Ahora la suma debería ser 1
@i
M=D                 // Aquí ya debería de sobrescribir la suma a la nueva

```
Acá ya tengo dudas de como ponerme a hacer el ciclo porque ya se me ocurre es hacer @2 y volver a copiar el último bloque pero creo que quedaría un código muy largo entonces voy a consultar.

```
@0                  // A es 0
D=A                 // D es 0
@i                  // Para guardar aquí la suma
M=D                 // En la posición i se guarda D que es 0

@0                  // A es 0
D=A                 // D es 0
@j                  // Aquí sería como para hacer un for en el que j empieza en 0
M=D                 // En la posición j se guarda el 0

```
Aquí volví a intentar el código 


Considera que los datos del arreglo están almacenados desde la dirección 16. Inicializa el arreglo en lenguaje ensamblador.
Simula paso a paso el programa en ensamblador. Recuerda la metodología: predice, ejecuta, observa y reflexiona.
Construye tu programa PASO A PASO mediante pruebas. Indica qué característica vas a implementar con cada prueba y cómo la probaste.
Muestra el programa final y cómo lo probaste.


