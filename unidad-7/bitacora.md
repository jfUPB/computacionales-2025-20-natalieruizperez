# Bitácora de aprendizaje de la unidad 7

## Actividad 01
**1. Incluye una captura de pantalla del ejemplo funcionando en tu máquina.**

<img width="1045" height="533" alt="image" src="https://github.com/user-attachments/assets/bb7d70ef-06c4-49ea-8e70-81fd52b0f52c" />

**2. Observa el proyecto, trata de entenderlo, pero ten presente que lo analizaremos más adelante.**

Voy a intentar entender qué sucede sin conocimientos previos, a simple vista creo que es un triángulo naranja y no parece que se pueda interactuar con él. lo único que veo es que al apretar escape se cierra la pestaña.


**3. ¿Qué preguntas te surgen al ver el código?. Anota al menos tres preguntas que te gustaría investigar más adelante (no te preocupes que la idea de esta unidad es que las resuelvas).**

1. En qué parte de la memoria se crea el triángulo?
2. Por qué el triángulo tiene un código tan largo a pesar de que parece que no se puede interactuar significativamente?
3. Veo que se usa mucho gl en el código y supongo que es debido a una biblioteca pero quiero saber por qué se usa esa en particular
   
---
## Actividad 02

**Te voy a pedir un resumen en tus propias palabras de lo que acabas de leer debes tratar de conectar GLFW, opengl32.lib, GLAD, GLM y los drivers de la GPU. ¿Qué rol cumple cada uno? ¿Cómo se relacionan entre sí? Mira, trata de hacer esto de memoria y como si estuvieras contándole a un amigo que quiere aprender OpenGL. Cuando haces el proceso de memoria tu cerebro hace un esfuerzo adicional y eso te ayuda a aprender. Además, si no recuerdas algo quiere decir que no lo entendiste bien y eso es una buena señal para que vuelvas a leerlo.**

Según lo que recuerdo GLM es la biblioteca que permite usar matemáticas y crear visuales, por otro lado GLFW sirve para que hayan ventanas, opengl32.lib me acuerdo que servía para algo pero no se usará en este caso. Por otro lado GLAD se usaba como para incluir bibliotecas y los drivers de la GPU permite que encontremos direcciones de memoria. Voy a volverlo a leer y luego a hacer un resumen conectando conceptos.

  En resumen, opengl32.lib no lo usaremos en este caso porque es una versión anterior y además la idea es poder usar los drivers de la gpu. Entonces teniendo en cuenta esos drivers pienso que al ejecutar el programa lo que se tiene que hacer es crear una ventana entonces por medio de GLFW es posible hacerlo, después a traves de GLAD es como puedo incluir funcioalidades que no aparecen inicialmente y por medio de GLM es como se crea la visual, como en el ejemplo que es un triángulo. 

---
## Actividad 03

**Qué tal si ensayas. Prueba con esta línea**
// 9) Configura el viewport
glViewport(0, 0, bufferWidth, bufferHeight);

**¿Qué pasa si?**
glViewport(0, bufferHeight/2, bufferWidth/2, bufferHeight/2);

<img width="931" height="492" alt="image" src="https://github.com/user-attachments/assets/2da5b6b5-def5-4f4a-a04a-36411379ad6b" />

  Cambia los valores de bufferWidth y bufferHeight: divide por 2, por 4, multiplica por 2, por 4, etc. ¿Qué pasa? ¿Qué observas? ¿Qué crees que está pasando?
  
  <img width="828" height="431" alt="image" src="https://github.com/user-attachments/assets/663f76ee-6017-4450-a84b-3a7521ee220d" />


 ** Realiza un resumen de lo que has aprendido hasta ahora, haciendo un diagrama conceptual o un mapa mental. Experimentando. ¿Cómo? Haciendo la pregunta mágica: ¿Qué pasaría si? ¿Qué pasaría si cambio el tamaño de la ventana? ¿Qué pasaría si cambio el tamaño del viewport? Entonces hagamos “digestión”: en tu bitácora, escribe un resumen de lo que has aprendido hasta ahora y piensa en un experimento del tipo ¿Qué pasaría si?**

 Qué pasaría si cambio esta línea 

c++
```
 if (!success) {
	glGetShaderInfoLog(vs, 512, nullptr, log);
	std::cerr << "ERROR VERTEX SHADER:\n" << log << "\n";
}

````
**Por**

c++
````
if (!success) {
	glGetShaderInfoLog(vs, 1080, nullptr, log);
	std::cerr << "ERROR VERTEX SHADER:\n" << log << "\n";
}
````
<img width="913" height="426" alt="image" src="https://github.com/user-attachments/assets/735729e0-90f2-49d6-9757-a84ecacd3fd2" />

Como vi que no pasó nada cambié en donde decía 512 por 1080 porque asumo que se trata de la resolución.

<img width="1044" height="539" alt="image" src="https://github.com/user-attachments/assets/d2786247-abb4-49d0-b178-22f74eda7615" />

Qué pasaría si se cambián los valores de los vértices? 

<img width="784" height="420" alt="image" src="https://github.com/user-attachments/assets/2dca021e-7873-4019-b11d-04118468efc8" />

Se crea otra figura, ya no es un triángulo equilátero si no que es un triángulo rectángulo.


**¿Qué pasa si cambias el primer parámetro de glDrawArrays a GL_LINES? ¿Qué pasa si lo cambias a GL_POINTS? ¿Qué pasa si cambias el tercer parámetro a 2? ¿Qué pasa si lo cambias a 4? En esta unidad no profundizaremos en los tipos de primitivas, pero es importante que entiendas que OpenGL puede dibujar diferentes tipos de primitivas (triángulos, líneas, puntos, etc.).**

**Es importante que intentes responder estos conceptos sin ver inicialmente tus notas. Trata de ejercitar tu memoria y tu comprensión. Luego, puedes revisar tus notas para completar o corregir lo que hayas escrito.**

1. ¿Qué es el contexto OpenGL?
2. ¿Cuál es el rol de la biblioteca GLFW y qué ventaja tiene usarla?
3. ¿Por qué crees que OpenGL necesita un contexto (recuerda la analogía del taller de arte)?
4. ¿En últimas qué será el framebuffer y a qué te recuerda de las dos primeras unidades del curso?
5. ¿Qué relación entre en el viewport y el framebuffer?
6. ¿En todo la analizado hasta ahora qué rol juega los drivers de la GPU y la GPU misma?
7. ¿Por qué crees que sea necesario activar el VSync? ¿Si no lo activas y la imagen es estática qué crees que pase, y si es dinámica?
8. En esta unidad estamos usando OpenGL moderno, pero ¿Qué es OpenGL Legacy? ¿Qué diferencias hay entre ambos?
9. ¿Qué es el shader program? ¿Por qué es importante en OpenGL moderno?
10. Trata de revisar el código setupTriangle(), intuitivamente ¿Qué crees que hace? ¿Qué crees que es el VAO y el VBO?
11. En el ciclo principal (game loop) de OpenGL, notaste que en cada frame (cuadro) le decimos a openGL que use el shader program y el VAO. Si le indicas esto antes del game loop ¿Será necesario seguirlo haciendo en cada loop? Si no es necesario ¿En qué casos crees que esto puede ser útil?
12. Finalmente, recuerda lo que hace glfwSwapBuffers(mainWindow); ¿Por qué crees que es importante? ¿Qué pasaría si no lo llamas? ¿Cómo explicas lo que pasa si no lo llamas? (experimenta)

---
## Actividad 04

**Luego de estudiar las unidades 1 y 2 de este curso y ver el video, escribe con tus propias palabras ¿Cuál es la diferencia entre una CPU y una GPU?**

Trata de responder de memoria a cada pregunta. No busques la respuesta en el video. Trata de recordar lo que viste. De todas maneras si no lo logras hacer, regresa al video y busca la respuesta.

1. ¿Cuáles son los tres pasos claves del pipeline de OpenGL? Explica en tus propias palabras cuál es el objetivo de cada paso.
2. La gran novedad que introduce OpenGL moderno es el pipeline programable. ¿Qué significa esto? ¿Qué diferencia hay entre el pipeline fijo y el programable? ¿Qué ventajas le ves a esto? y si el pipeline es programable, ¿Qué tengo que programar?
3. Si fueras a describir el proceso de rasterización ¿Qué dirías?
4. ¿Qué son los fragmentos? ¿Es lo mismo un fragmento que un pixel? ¿Por qué?
5. Explica qué problema resuelve el Z-buffer y ¿Qué es el depth test?
6. ¿Por qué se presenta el problema de la aliasing? ¿Qué es el anti-aliasing?
7. ¿Qué relación hay entre la iluminación y el fragment shader? Siempre es necesario tener en cuenta la iluminación en un fragment shader? o puedo hacer un fragment shader sin iluminación? Explica que implicaciones tiene esto.
8. ¿Qué implica para la GPU que una aplicación tenga múltiples fuentes de iluminación?


**Escribe un resumen en tus propias palabras de lo que se necesita para dibujar un triángulo en OpenGL.**
**Escribe un resumen en tus propias palabras de lo que necesitas para poder usar un shader en OpenGL.**

**Implementa el código anterior en tu máquina y captura pantalla del resultado. Pero antes de hacerlo trata de predecir qué va a pasar.**

---
##Actividad 05
