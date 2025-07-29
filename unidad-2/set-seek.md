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

### Actividad 02
**1. Modifica el programa anterior para que dibuje una línea horizontal negra de 16 pixeles de largo en la esquina superior izquierda de la pantalla. (Recuerda que cada word en la memoria representa 16 pixeles).**


``` 
@SCREEN  //Es 16384
M=1    // En la posición de screen guarda uno y se ve un pixel
``` 

** Traduce este programa a lenguaje C++ para que relaciones cómo los conceptos de alto nivel se traducen a bajo nivel.**


ACTIVIDAD 4 y 5


``` 
