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
M= 1    // En la posición de screen guarda uno y se ve un pixel
```
<img width="634" height="131" alt="image" src="https://github.com/user-attachments/assets/27835f1b-e326-4f29-8081-ff00cee125fd" />

  En la foto se puede ver el pixel y cómo se guarda en la posición de la memoria el valor 1.

**2. Traduce este programa a lenguaje C++ para que relaciones cómo los conceptos de alto nivel se traducen a bajo nivel.**

No tenía claro como empezar a programarlo en c++ ya que los lenguajes que usamos el semestre pasado eran python y c# que es el que usa unity. Pienso que para crearlo en c++ debe de tener una lógica similar pero como es otro lenguaje una forma de llamar las variables que desconozco.

``` c
screen = -1;        // Le fuerza al compilador para que asigne la variable a 16384
screen = 0xFFFF;    // En lo mismo que -1
``` 
  Este es el que hicimos en clase y lo que hacía era encender pixeles así que creo que para hacer lo mismo en c que el còdigo anterior se haría así:
¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡¡

---
### Actividad 02
**1. Modifica el programa anterior para que dibuje una línea horizontal negra de 16 pixeles de largo en la esquina superior izquierda de la pantalla. (Recuerda que cada word en la memoria representa 16 pixeles).**

Esta es la predicción.

``` 
@SCREEN  //Es 16384
M=?   // En M se le debe de asignar un número que desconozco
```
Se pone 0 ya que quiero apagar los píxeles. Por ejemplo, en la actividad anterior se ponía -1 porque 
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

Para hacer que funcione con el teclado es necesario acceder a @KBD entonces pienso que primero debo de buscar como se escribe d e i en KBD y luego poner las condiciones para que sepa el programa cuando usar cual.
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

Código en c++
``` c++
int tmp
while(1)
{
tmp = KDB;

if(tmp ==100){
//DERECHA
}
elsee if(tmp ==105){
//IZQUIERDA
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

``` 
int a = 10;
int* p;        // Declaro nueva variable p que es un puntero
p = &a;        // Luego la defino y estoy guardando la dirección de a
*p = 20;       // Modificando la variable a través del puntero y el 10 se vuelve 20
``` 

``` 
int a = 10;
int b = 5;
int *p;        // Declarando p
p = &a;        // Luego en p guardo la dirección de la a
b = *p;        // Se lee el contenido de a porque es el contenido de la variable a la que apunto
```

El 5 que teníamos antes se convierte en un 10 en la última línea del código.

**Código en lenguaje ensamblador**
Hipótesis
```
@10
D-A
arroba a
m igual a d


arroba a
d igual a a
p arroba
m igual a d

arroba 20
d igual a a
arroba p
A=M
M=D

en la dirrecion 16 de la ram deberia aparecer el 10
despues de ejecutar las dos instrucciones deberia de apaarecer la dirrecion de a (16) en la 17



``` 

En lenguaje ensamblador
@i
M=1
@sum
M=0

(WHILE)     //Etiqueta para mostrar que se viene un ciclo


@WILE
0;JMP




