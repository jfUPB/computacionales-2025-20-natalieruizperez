# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01
Recuerda la metodología: predice, ejecuta, observa y reflexiona.

**1. Escribe un programa que dibuje un punto negro en la esquina superior izquierda de la pantalla. (Recuerda que la esquina superior izquierda corresponde al primer bit del primer word en la dirección SCREEN).**

Aquí quise intentar hacerlo.
```
@SCREEN
D=A
@i
M=D
```
Me di cuenta que estaba cometiendo un gran error y era pnsar que tenía que guardar el valor de screen, para poder crear un pixel lo que en realidad tengo que hacer es  guardar la memoria en la parte de screen el pixel que desee.

```
@SCREEN  //Es 16384
M=1    // En la posición de screen guarda uno y se ve un pixel
```
<img width="634" height="131" alt="image" src="https://github.com/user-attachments/assets/27835f1b-e326-4f29-8081-ff00cee125fd" />
En la foto se pede ver el pixel y cómo se guarda en la posición de la memoria el valor 1.

**2. Traduce este programa a lenguaje C++ para que relaciones cómo los conceptos de alto nivel se traducen a bajo nivel.**

``` c#

``` 

``` c#
screen = -1;        //Le fuerza al compilador para que asigne la variable a 16384
screen = 0xFFFF;
``` 

---
### Actividad 02
**1. Modifica el programa anterior para que dibuje una línea horizontal negra de 16 pixeles de largo en la esquina superior izquierda de la pantalla. (Recuerda que cada word en la memoria representa 16 pixeles).**


``` 
@SCREEN  //Es 16384
M=1    // En la posición de screen guarda uno y se ve un pixel
``` 

** Traduce este programa a lenguaje C++ para que relaciones cómo los conceptos de alto nivel se traducen a bajo nivel.**


---
### Actividad 04
Enunciado
``` 
//Adds 1+...+100.
 int i=1;
 int sum=0;

 while(i <=100){
    sum+= i;
    i++;
 }
```
@i
M=1
@sum
M=0

(WHILE)     //Etiqueta para mostrar que se viene un ciclo


@WILE
0;JMP
```



 Se traduce a ensamblador como 
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

El progrma ensamblador tiene que ser el mismo ya que son dos formas distintas de escribirlo.

Simulación tiene que ser con predección, análisis y conclusión. Qué conclusiones has sacado
Son programas equivalentes y hacen lo mismo, por lo tanto deberían de tener un código ensamblador igual. El compilador saben que ambo son lo mismo.

Un puntero es una variable en la que se guardan direcciones.


``` 
int i = 5;          // Int i variable en la que se guarda un valor entero
int* ptr = &i;      // ptr guarda la dirección de un objeto, un flotante u otra cosa por lo que hay que especificar que tipo de dirección es.
Para invocar una dirección le pongo la "&" adelante.

``` 
### Actividad 05
Interpretación de código.

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



``` 




