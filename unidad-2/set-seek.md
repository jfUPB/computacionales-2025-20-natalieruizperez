# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01
Recuerda la metodología: predice, ejecuta, observa y reflexiona.

**1. Escribe un programa que dibuje un punto negro en la esquina superior izquierda de la pantalla. (Recuerda que la esquina superior izquierda corresponde al primer bit del primer word en la dirección SCREEN).**

Aquí quise intentar hacerlo pero no funcionó.
```
@SCREEN        //A es 16384
D=A            // D es A
@i             // A es 16
M=D            // En la dirección 16 se guarda 16384
```
Al desarrollarlo en clase me di cuenta que estaba cometiendo un gran error y era pnsar que tenía que guardar el valor de screen, para poder crear un pixel lo que en realidad tengo que hacer es  guardar en la dirección de screen un pixel.

```
@SCREEN  //Es 16384
M=1    // En la posición de screen guarda uno y se ve un pixel
```
<img width="634" height="131" alt="image" src="https://github.com/user-attachments/assets/27835f1b-e326-4f29-8081-ff00cee125fd" />

  En la foto se puede ver el pixel y cómo se guarda en la posición de la memoria el valor 1.

**2. Traduce este programa a lenguaje C++ para que relaciones cómo los conceptos de alto nivel se traducen a bajo nivel.**

No tenía claro como empezar a programarlo en c++ ya que los lenguajes que usamos el semestre pasado eran python y c# que es el que usa unity. Pienso que para crearlo en c++ debe de tener una lógica similar, este es el que hicimos en clase.

``` c
screen = -1;        // Le fuerza al compilador para que asigne la variable a 16384
screen = 0xFFFF;    // En lo mismo que -1
```
 
---
### Actividad 02
**1. Modifica el programa anterior para que dibuje una línea horizontal negra de 16 pixeles de largo en la esquina superior izquierda de la pantalla. (Recuerda que cada word en la memoria representa 16 pixeles).**

Esta es la predicción.

``` 
@SCREEN  //Es 16384
M=?   // En M se le debe de asignar un número que desconozco
```
Se pone 0 ya que quiero apagar los píxeles. 
``` 
@SCREEN  //Es 16384
M=0   
```
<img width="1823" height="345" alt="image" src="https://github.com/user-attachments/assets/72527ffd-aa31-4687-8c13-40be4e53f0a3" />

**Traduce este programa a lenguaje C++ para que relaciones cómo los conceptos de alto nivel se traducen a bajo nivel.**
Teniendo en cuenta el ejercicio anterior pienso que seguiría la misma lógica entonces usé el código pasado y puse todo en 0.

``` 
screen = 0x0000;   
```

---
### Actividad 03
Modifica el programa de la actividad anterior de tal manera que puedas mover la línea horizontal de derecha a izquierda usando las teclas d y i respectivamente. Tu programa no tiene que verificar si la línea se sale de la pantalla.

  Este es el ejercicio que hicimos en clase:
  
```
@SCREEN
M=-1
@CONTADOR 
M=0


(DERECHA)

//Borrar posición actual
@CONTADOR
D=M          // D es contador
@SCREEN
A=D+A        // A es contador + screen
M=0          // Para apagar

@CONTADOR    
M=M+1       // Se le suma al contador uno
D=M         // D es M
@SCREEN     // A es screen
A=D+A       // Se le suma a la pantalla el nuevo contadoor
M=-1        // Para prender

(IZQUIERDA) // Toda esta parte hace lo mismo que la derecha

@CONTADOR
D=M
@SCREEN
A=D+A
M=0

@CONTADOR 
M=M-1       // A diferencia que el de la derecha se le resta uno para que vaya a la izquierda
D=M
@SCREEN
A=D+A
M=-1

@IZQUIERDA
0;JMP
```

Para hacer que funcione con el teclado es necesario acceder a @KBD entonces pienso que primero debo de buscar como se escribe d e i en KBD y luego poner las condiciones.
```
@SCREEN
M=-1
@CONTADOR 
M=0

@100         // Es d
D=A          // D es A
@KBD         // A es 24576
M=D          // En esa posición guardo D y creo que así puedo para acceder a esa tecla en específico
@DERECHA     // Salta a la etiqueta
D;JEQ

@105         // Es i y me di cuenta quesi cuento a partir de d en orden alfabético son 5 letras
D=A          // D es A
@KBD         // A es 24576
M=D          // En esa posición guardo D y creo que así puedo para acceder a esa tecla en específico
@IZQUIERDA   // Salta a la etiqueta 
D;JEQ        

(DERECHA)

//Borrar posición actual
@CONTADOR
D=M          // D es contador
@SCREEN
A=D+A        // A es contador + screen
M=0          // Para apagar

@CONTADOR    
M=M+1       // Se le suma al contador uno
D=M         // D es M
@SCREEN     // A es screen
A=D+A       // Se le suma a la pantalla el nuevo contadoor
M=-1        // Para prender

(IZQUIERDA) // Toda esta parte hace lo mismo que la derecha

@CONTADOR
D=M
@SCREEN
A=D+A
M=0

@CONTADOR 
M=M-1       // A diferencia que el de la derecha se le resta uno para que vaya a la izquierda
D=M
@SCREEN
A=D+A
M=-1

@IZQUIERDA
0;JMP
```

Al analizar mi hipótesis me doy cuenta que esta erronea porque no se pueden guardar valores en la dirección del teclado, tenía un error conceptual. Inicialmente pensé que era posible hacerlo porque estaba teniendo en cuenta como trabajamos con screen pero son cosas diferentes. También se me olvidó comparar los valores.
```
@SCREEN
M=-1
@CONTADOR 
M=0

(LOOP)       // Para hacer un ciclo
@KBD
D=M          // Para saber qué tecla se presiona

@100         // Es d
D=D-A        // Da 0 si se está presionando la d
@DERECHA     // Salta a la etiqueta
D;JEQ        // Para ver si D es 0


@KBD         // Vuelvo a poner lo mismo pero esta vez para hacerlo con i
D=M          // Para saber qué tecla se presiona

@105         // Es i y me di cuenta quesi cuento a partir de d en orden alfabético son 5 letras
D=D-A        // Da 0 si se está presionando la i
@IZQUIERDA   // Salta a la etiqueta 
D;JEQ        // Para ver si D es 0

@LOOP
0;JMP

(DERECHA)

@CONTADOR
D=M          // D es contador
@SCREEN
A=D+A        // A es contador + screen
M=0          // Para apagar

@CONTADOR    
M=M+1       // Se le suma al contador uno
D=M         // D es M
@SCREEN     // A es screen
A=D+A       // Se le suma a la pantalla el nuevo contadoor
M=-1        // Para prender

(IZQUIERDA) // Toda esta parte hace lo mismo que la derecha

@CONTADOR
D=M
@SCREEN
A=D+A
M=0

@CONTADOR 
M=M-1       // A diferencia que el de la derecha se le resta uno para que vaya a la izquierda
D=M
@SCREEN
A=D+A
M=-1

@IZQUIERDA
0;JMP
```

Ahora al programarlo en el otro lenguaje creo que quedaría algo así

```
screen = 0xFFFF;   
contador = 0;
// Bucle       
while (true) {
    if (kbd == 100) {         // Si se apreta d
        screen[contador] = 0;      // Apaga pixel
        contador =  contador + 1;        // Se le suma uno y va a la derecha
        screen[contador] = 0xFFFF; // Muestra donde queda
    }

    if (kbd == 105) {         //  Si se apreta i
        screen[contador] = 0;      // Apaga pixel
        contador = contador - 1;        // Se le resta uno y va a la izquierda
        screen[contador] = 0xFFFF; // Muestra donde queda
    }
}

```
Al comparar ambos lenguajes me doy cuenta que es posible obtener un resultado más corto al no usar el lenguaje ensamblador ya que este otro es con más estructura.

---

### Actividad 04
Convierte un ciclo while en un ciclo for

  Se observa este programa 
  
``` 
//Adds 1+...+100.
 int i=1;
 int sum=0;

 while(i <=100){
    sum+= i;
    i++;
 }
```

Que se traduce a ensamblador como 
```
 // Adds1+...+100.
 @i // i refers to some memory location.
 M=1 // i=1
 @sum // sum refers to some memory location.
 M=0 // sum=0
 (LOOP)
 @i
 D=M // D=i
 @100
 D=D-A // D=i-100
 @END
 D;JGT // If(i-100)>0 gotoEND
 @i
 D=M // D=i
 @sum
 M=D+M // sum=sum+i
 @i
 M=M+1 // i=i+1
 @LOOP
 0;JMP // GotoLOOP
 (END)
 @END                  //Instrucción de escape
 0;JMP // Infinite loop

 Programa equivalente
//Adds 1+...+100.
int sum=0;
for(int i = 1; i <=100; i++){
   sum+= i;
}
```

Ahora teniendo este programa hay que pasarlo a lenguaje ensamblador
```
//Adds 1+...+100.
int sum=0;
for(int i = 1; i <=100; i++){
   sum+= i;
}
```

Al analizar ambos programas en lenguaje ensamblador me doy cuenta que son muy parecidos porque en el lenguaje ensablador no hay ciclos for o while así que es lo mismo porque siguen la misma lógica pero tienen distintas formas de escribirlo. Eso pasa porque como el lenguaje ensamblador es de bajo nivel puede recibir y procesar instrucciones simples, en cambio las de alto nivel usan otras formas de escribir el código como más resumida.

En conclusión son programas equivalentes y hacen lo mismo, por lo tanto deberían de tener un código ensamblador igual. El compilador saben que son iguales.

### Actividad 05
Interpretación de código.

Un puntero es una variable en la que se guardan direcciones.

``` 
int i = 5;          // Int i variable en la que se guarda un valor entero
int* ptr = &i;      // ptr guarda la dirección de un objeto, un flotante u otra cosa por lo que hay que especificar que tipo de dirección es.
Para invocar una dirección le pongo la "&" adelante. 

```
Código del enunciado
``` 
int a = 10;
int* p;        // Declaro nueva variable p que es un puntero
p = &a;        // Luego la defino y estoy guardando la dirección de a
*p = 20;       // Modificando la variable a través del puntero y el 10 se vuelve 20
``` 
Esta es la hipótesis de cómo se haría en lenguaje ensamblador

```
@10           //A es 10
@PUNTERO      // Aquí estoy creando la variable de puntero
A=M           // Para guardar la A en P
@20           // A es 20
A=M           // Para que se guarde el 20 en p
``` 
Está mala mi hipótesis ya que por intentar seguir el código de arriba al pie de la letra me distraje y olvidé los principios entonces sobreescribí A pensando en que estaba creando variables. Tampoco se guarde a en la memoria. El código corregido quedaría así

```
// int a = 10
@10       // A es 10
D=A       // D es 10
@a 
M=D       // Se guarda el 10 en a

// int* p;
// p = &a;
@a       
D=A      // En D pone a
@p       
M=D     // Guarda a en p

// *p = 20;
@20      // A es 20
D=A      // D es 20
@p       
A=M     // A es lo que está guardado en p que es a
M=D     // a es 20

```

Este es el otro código que hay que pasar a lenguaje ensamblador
``` 
int a = 10;
int b = 5;
int *p;        // Declarando p
p = &a;        // Luego en p guardo la dirección de la a
b = *p;        // Se lee el contenido de a porque es el contenido de la variable a la que apunto
```
Mi hipótesis es la siguiente.
```
// int a = 10;
@10          // A es 10
D=A          // D es 10
@a
M=D          // Se guarda 10 en a

// int b = 5;
@5           // A es 5
D=A          // D es 5
@b            
M=D          // Se guarda 5 en b

// int *p;
// p = &a;
// Esta parte es la misma que la de arriba
@a
D=A          
@p
M=D          


// b = *p;
@p
D=A         // D es p
@b            
M=A         // Se guarda b


```

Veo que hacer el ejercicio pasado me sirvió para entender la lógica del principio del programa pero todavía tengo vacíos al final. Veo que en mi hipótesis me equivoqué en la forma de acceder al valor del puntero, como lo hice no tuve en cuenta el valor si no la dirección. 

```
// int a = 10;
@10          // A es 10
D=A          // D es 10
@a
M=D          // Se guarda 10 en a

// int b = 5;
@5           // A es 5
D=A          // D es 5
@b            
M=D          // Se guarda 5 en b

// int *p;
// p = &a;
// Esta parte es la misma que la de arriba
@a
D=A          
@p
M=D          

// b = *p;    // Lee el valor apuntado por p (que es a) y lo guarda en b
@p
A=M         
D=M          
@b
M=D         // En b se guarda el valor de D 

```
Un puntero guarda la dirección de otra variable y también permite acceder o cambiar su valor. En lenguaje ensamblador hay que hacer todo paso a paso, pero en otros lenguajes de programación es más fácil porque se usan símbolos. En cambio, en ensamblador todo se hace manualmente. Los ejercicios me sirvieron para entender mejor cómo funciona la memoria y también para aprender a interpretar códigos y pasarlos a otros lenguajes.




