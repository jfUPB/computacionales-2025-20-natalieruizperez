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

**Crear un proyecto openGL en Windows**
1. Cree un proyecto vacio de c++

   <img width="933" height="988" alt="image" src="https://github.com/user-attachments/assets/59ac6046-e8db-4592-a61f-ae5138dcf829" />

2. Después agregue la carpeta external y dentro glfw34, glad y glm-101-light.

<img width="632" height="295" alt="image" src="https://github.com/user-attachments/assets/edce4556-fb50-4a45-b0a2-e036258c239e" />

3. Le di a glfw4 available for download y luego a 64-bit windows binaries, lo descomprimi y guarde las carpetas necesarias en glfw34.

<img width="327" height="460" alt="image" src="https://github.com/user-attachments/assets/f928e37c-85e4-4a3c-ad57-c4a182bf7aa9" />

<img width="925" height="244" alt="image" src="https://github.com/user-attachments/assets/6a9d3044-bca6-40b3-b78a-5e342a7a68cf" />

<img width="793" height="353" alt="image" src="https://github.com/user-attachments/assets/230381f8-f915-49ac-9a19-6922bc9337a3" />


4. Fui a la página de GLAD para poder acceder a funciones en tiempo de ejecución y puse las siguientes cosas. Le di a generate, descargué el zip y puse las carpetas en glad.


<img width="895" height="923" alt="image" src="https://github.com/user-attachments/assets/47f3517b-fe33-4802-9a44-cbbca713507b" />

<img width="828" height="458" alt="image" src="https://github.com/user-attachments/assets/de41c252-2b9f-4fc2-9219-df61330f3037" />

<img width="787" height="296" alt="image" src="https://github.com/user-attachments/assets/38858387-23bb-4dbb-8ae0-928e133ef5e7" />

5. Para poner la dependencia de GLM fui al githhb y descargué el zip y puse la carpeta de glm del zip en el external.

<img width="879" height="195" alt="image" src="https://github.com/user-attachments/assets/898c1acc-7874-4c47-912e-d19ec4d39ac8" />

<img width="751" height="627" alt="image" src="https://github.com/user-attachments/assets/d78cde51-4270-4ae4-b662-61a72bfa3027" />

6. Faltaba el código y no me salía el menu desplegable de c/c++ entonces descargué el cpp y lo puse en la carpeta del proyecto. Luego le di click detecho en el proyecto, NO EN LA SOLUCIÓN, le di a agregar y seleccioné el triángulo cpp.

<img width="719" height="392" alt="image" src="https://github.com/user-attachments/assets/99cd6685-bf8a-4c6a-9dd6-8c1999fe892f" />

7. Ahora para poder enlazar todo con las dependencias le di a click derecho en el proyecto y después propiedades. Y en el de c/c++ puse incluir directorios, le di a editar. Después se creo una nueva pestaña y para vincularlo le di a la nueva carpeta, en la parte derecha salen 3 puntos para vincularlo.

<img width="782" height="532" alt="image" src="https://github.com/user-attachments/assets/58c2bf96-25a8-439c-a4b6-ef0868a2e6b6" />

<img width="784" height="534" alt="image" src="https://github.com/user-attachments/assets/0987f819-5888-4a86-b8e6-acf7bedac0e8" />

<img width="476" height="481" alt="image" src="https://github.com/user-attachments/assets/c0367a9a-eaf6-440c-abf4-7e4f6cd30f2a" />


<img width="897" height="663" alt="image" src="https://github.com/user-attachments/assets/02076275-fd01-49e5-8889-85a121e8ef44" />


8. Ya funciona

<img width="948" height="980" alt="image" src="https://github.com/user-attachments/assets/d73064be-3336-4a6e-85b1-b73c2a63e15b" />

**Te voy a pedir un resumen en tus propias palabras de lo que acabas de leer debes tratar de conectar GLFW, opengl32.lib, GLAD, GLM y los drivers de la GPU. ¿Qué rol cumple cada uno? ¿Cómo se relacionan entre sí? Mira, trata de hacer esto de memoria y como si estuvieras contándole a un amigo que quiere aprender OpenGL. Cuando haces el proceso de memoria tu cerebro hace un esfuerzo adicional y eso te ayuda a aprender. Además, si no recuerdas algo quiere decir que no lo entendiste bien y eso es una buena señal para que vuelvas a leerlo.**

Según lo que recuerdo GLM es la biblioteca que permite usar matemáticas y crear visuales, por otro lado GLFW sirve para que hayan ventanas, opengl32.lib me acuerdo que servía para algo pero no se usará en este caso. Por otro lado GLAD se usaba como para incluir bibliotecas y los drivers de la GPU permite que encontremos direcciones de memoria. Voy a volverlo a leer y luego a hacer un resumen conectando conceptos.

  En resumen, opengl32.lib no lo usaremos en este caso porque es una versión anterior y además la idea es poder usar los drivers de la gpu. Entonces teniendo en cuenta esos drivers pienso que al ejecutar el programa lo que se tiene que hacer es crear una ventana entonces por medio de GLFW es posible hacerlo, después a traves de GLAD es como puedo incluir funcioalidades que no aparecen inicialmente y por medio de GLM es como se crea la visual, como en el ejemplo que es un triángulo. 

## Actividad 03

**Qué tal si ensayas. Prueba con esta línea**
// 9) Configura el viewport
glViewport(0, 0, bufferWidth, bufferHeight);

**¿Qué pasa si?**
glViewport(0, bufferHeight/2, bufferWidth/2, bufferHeight/2);

<img width="931" height="492" alt="image" src="https://github.com/user-attachments/assets/2da5b6b5-def5-4f4a-a04a-36411379ad6b" />

  Cambia los valores de bufferWidth y bufferHeight: divide por 2, por 4, multiplica por 2, por 4, etc. ¿Qué pasa? ¿Qué observas? ¿Qué crees que está pasando?
  
  <img width="828" height="431" alt="image" src="https://github.com/user-attachments/assets/663f76ee-6017-4450-a84b-3a7521ee220d" />


 **Realiza un resumen de lo que has aprendido hasta ahora, haciendo un diagrama conceptual o un mapa mental. Experimentando. ¿Cómo? Haciendo la pregunta mágica: ¿Qué pasaría si? ¿Qué pasaría si cambio el tamaño de la ventana? ¿Qué pasaría si cambio el tamaño del viewport? Entonces hagamos “digestión”: en tu bitácora, escribe un resumen de lo que has aprendido hasta ahora y piensa en un experimento del tipo ¿Qué pasaría si?**

Es necesario asegurarse de que el programa cuente con todos los elementos necesarios para poder hacer que el código funcione, o si no, no se ejecutará correctamente. GLFW es la biblioteca para crear la ventana eso hace que haya en donde dibujar. GLAD es una biblioteca que usamos para agregar a cosas de OpenGL, tengo que volver a revisar los conceptos porque no recuerdo el nombre de esas "cosas". GLM es una biblioteca de matemáticas que sirve para trabajar con operaciones más fácilmente. Los drivers de la GPU ejecutan las instrucciones de OpenGL. Cuando experimenté con glViewport, entendí que esa función define qué parte de la ventana se usará para renderizar la imagen. T

 ---

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

Luego de hablar con el profe me sugirió que no cambiara los parámetros del shader ya que podía ocasionar que el programa dejara de funcionar. Tengo que centrarme más en lo que pide cada actividad, en este caso los ejeplos que muestra en el enunciado están relacionados unicamente con el viewport y la figura.

**¿Qué pasa si cambias el primer parámetro de glDrawArrays a GL_LINES? ¿Qué pasa si lo cambias a GL_POINTS? ¿Qué pasa si cambias el tercer parámetro a 2? ¿Qué pasa si lo cambias a 4? En esta unidad no profundizaremos en los tipos de primitivas, pero es importante que entiendas que OpenGL puede dibujar diferentes tipos de primitivas (triángulos, líneas, puntos, etc.).**

**GL_LINES**
Se crea una línea
<img width="896" height="671" alt="image" src="https://github.com/user-attachments/assets/3a31f41a-f77e-4931-890c-1a20b65675c7" />

**GL_POINTS**
Se crea un punto pequeño
<img width="778" height="670" alt="image" src="https://github.com/user-attachments/assets/0d41bb96-e3fa-4921-967c-bd5fe1378106" />

**Cambiando el último parámetro a 2**
Se crean dos puntos
<img width="806" height="685" alt="image" src="https://github.com/user-attachments/assets/d3ade853-5fb7-498f-a0ec-2f7f73645ae1" />

De esto puedo concluir que se puede empezar con un tipo de figura gracias a GL_.

---

**Es importante que intentes responder estos conceptos sin ver inicialmente tus notas. Trata de ejercitar tu memoria y tu comprensión. Luego, puedes revisar tus notas para completar o corregir lo que hayas escrito.**

**1. ¿Qué es el contexto OpenGL?**

Es una especie de lugar que permite manejar todo de forma sencilla, en esta están los shaders, el tipo de figura y colores que permiten que funcione el programa.

**2. ¿Cuál es el rol de la biblioteca GLFW y qué ventaja tiene usarla?**

El rol de la biblioteca GLFW es que una biblioteca que permite crear una ventana es útil porque así es como se puede ver qué se ejecuta.

**3. ¿Por qué crees que OpenGL necesita un contexto (recuerda la analogía del taller de arte)?**

OpenGL necesita un contexto para saber en qué parte hace cada cosa.

**4. ¿En últimas qué será el framebuffer y a qué te recuerda de las dos primeras unidades del curso?**

La verdad no recuerdo que es framebuffer así que miraré las notas para refrescar la memoria. El framebuffer es donde OpenGL pinta cada cuadro.

**5. ¿Qué relación entre en el viewport y el framebuffer?**

El viewport es el área del framebuffer mientras que el framebuffer es donde se pinta, si se configura mal entonces la figura se podria ver estirada.

**6. ¿En todo la analizado hasta ahora qué rol juega los drivers de la GPU y la GPU misma?**

Son una especie de intermediarios para que la GPU pueda interpretar el código y hacer los cálculos necesarios.

**7. ¿Por qué crees que sea necesario activar el VSync? ¿Si no lo activas y la imagen es estática qué crees que pase, y si es dinámica?**

Se necesita VSync para que pueda haber sincronización, si no se activa cuando la imagen es estática no creo que haya un cambio significativo peor si es dinámica y no está activado podría verse mal y no como se supone que actuaría.

**8. En esta unidad estamos usando OpenGL moderno, pero ¿Qué es OpenGL Legacy? ¿Qué diferencias hay entre ambos?**

Esto no lo recuerdo entonces volveré a revisar la actividad y a consultar al respecto. Luego de investigar OpenGL Legacy es una versión más antigua de OpenGL y la diferencia es que en OpenGL Legacy se dibujaba con glBegin(), glVertex3f(), y glEnd(), en cambio en el actual se usan shaders.

**9. ¿Qué es el shader program? ¿Por qué es importante en OpenGL moderno?**

Un shader program le dicen a la GPU cómo hacer las cosas. Es fundamental en OpenGL moderno porque gracias a los shaders es posible dibujar.

**10. Trata de revisar el código setupTriangle(), intuitivamente ¿Qué crees que hace? ¿Qué crees que es el VAO y el VBO?**

Crep que es para preparar el triángulo con los datos necesarios como la posición de los vértices. La verdad no tengo idea de qué es VAO y VBO entonces voy a consultar y revisar la actividad. Luego de buscar encontré que VAO significa Vertex Array Object y se encarga de guardar todo lo necesario para crear el triángulo en cambio VBO que singifica Vertex Buffer Object y es donde se guardan los datos de los vértices.

**11. En el ciclo principal (game loop) de OpenGL, notaste que en cada frame (cuadro) le decimos a openGL que use el shader program y el VAO. Si le indicas esto antes del game loop ¿Será necesario seguirlo haciendo en cada loop? Si no es necesario ¿En qué casos crees que esto puede ser útil?**

Pensaría que no es necesario porque al fin de al cabo es un loop entonces no veo la necesidad de además de escribirlo en el loop hacerlo al principio. Puede ser útil quizás cuando se escriben muchas instrucciones para evitar errores y asegurarse de que el programa funcione correctamente.

**12. Finalmente, recuerda lo que hace glfwSwapBuffers(mainWindow); ¿Por qué crees que es importante? ¿Qué pasaría si no lo llamas? ¿Cómo explicas lo que pasa si no lo llamas? (experimenta)**

glfwSwapBuffers(mainWindow) es importante porque muestra lo que se hizo en framebuffer que OpenGL acaba de renderizar. Borré la línea y al hacerlo no se ve el triángulo, la pestaña sale en blanco.

<img width="870" height="617" alt="image" src="https://github.com/user-attachments/assets/139c6b16-814b-41f1-80e5-332af997658b" />

---
## Actividad 04

**Luego de estudiar las unidades 1 y 2 de este curso y ver el video, escribe con tus propias palabras ¿Cuál es la diferencia entre una CPU y una GPU?**

La diferencia entre CPU y GPU es que la GPU se encarga del procesamiento de texturas y vértices, las renderiza, en cambio la CPU es el que se encarga de manejar las tareas.

**Trata de responder de memoria a cada pregunta. No busques la respuesta en el video. Trata de recordar lo que viste. De todas maneras si no lo logras hacer, regresa al video y busca la respuesta.**

**1. ¿Cuáles son los tres pasos claves del pipeline de OpenGL? Explica en tus propias palabras cuál es el objetivo de cada paso.**

Los tres pasos clave de OpenGL son vertex shading, rasterization y fragment shading.

**2. La gran novedad que introduce OpenGL moderno es el pipeline programable. ¿Qué significa esto? ¿Qué diferencia hay entre el pipeline fijo y el programable? ¿Qué ventajas le ves a esto? y si el pipeline es programable, ¿Qué tengo que programar?**

Significa que ahora se puede acceder al funcionamiento interno del pipeline, en cambio en el fijo no se podía y se tenía que trabajar con lo ya existente. La ventaja de que sea progamable es que és posible realizar efectos más avanzados. Se tienen que programar el vertex shader y pensará que el fragment shading también.

**3. Si fueras a describir el proceso de rasterización ¿Qué dirías?**

Consiste en que el programa analice en qué partes hay triángulos, después de eso se calcule la cantidad de pixeles que hay en esa zona. La GPU cálcula cuáles pixeles están cubiertos y luego le asigna un color.
   
**4. ¿Qué son los fragmentos? ¿Es lo mismo un fragmento que un pixel? ¿Por qué?**

Los fragmentos son grupos de píxeles, no es lo mismo un fragmento que un pixel porque el primero es un grupo y el segundo es solo una cosa.

**5. Explica qué problema resuelve el Z-buffer y ¿Qué es el depth test?**

El z-buffer resuelve problemas que pueden haber a la hora de renderizar varios objetos. Por ejemplo cuando se ve un objeto en el render la parte trasera no aparece esto es porque el z-buffer detecta que tiene un objeto delante de otro. Entonces en el caso de tener un objeto encima de otro, el objeto que esté más cerca de la cámara es el que se verá.
   
**6. ¿Por qué se presenta el problema de la aliasing? ¿Qué es el anti-aliasing?**

El problema del aliasing se presenta porque cuando un triángulo pasa por la mitad de un pixel puede dar como resultado una imagen pixelada. El anti-aliasing lo que hace es crear una cuadrícula de 16 y si pasa el triángulo por la mitad el programa lo analia y hace que se creen bordes con menos opacioadad para que la imagen se vea más suave.
    
**7. ¿Qué relación hay entre la iluminación y el fragment shader? Siempre es necesario tener en cuenta la iluminación en un fragment shader? o puedo hacer un fragment shader sin iluminación? Explica que implicaciones tiene esto.**

La relación entre iluminación y fragmnent shader es que cada uno depende del otro, puede haber iluminación sin fragment shader pero entonces siemrpre estaría brillante el objeto y también puede haber fragment shader sin iluminación pero no se vería absolutamente nada. La iluminación tiene que ver con el lugar en dodne está la luz, en cambio fragment shading que son varios pixeles en grupo y según la posición, rotación del objeto y la luz que recae sobre él los materiales del objeto se ven afectados.
    
**8. ¿Qué implica para la GPU que una aplicación tenga múltiples fuentes de iluminación?**

Para la GPU implica más trabajo ya que tendría que hacer más cálculos.

**Escribe un resumen en tus propias palabras de lo que se necesita para dibujar un triángulo en OpenGL.**

Necesito shaders, las coordenadas del triángulo para que el programa sepa donde dibujarlo, un compilador de shaders y una función para dibujar.

**Escribe un resumen en tus propias palabras de lo que necesitas para poder usar un shader en OpenGL.**

Para poder usar un shader en OpenGL es necesario enteder cómo funciona para poder saber qué partes modificar.  

**Implementa el código anterior en tu máquina y captura pantalla del resultado. Pero antes de hacerlo trata de predecir qué va a pasar.**


```c++
#include <iostream>
#include <glad/glad.h>
#include <GLFW/glfw3.h>

void framebuffer_size_callback(GLFWwindow* window, int width, int height) {
	glViewport(0, 0, width, height);
}

void processInput(GLFWwindow* window) {
	if (glfwGetKey(window, GLFW_KEY_ESCAPE) == GLFW_PRESS)
		glfwSetWindowShouldClose(window, true);
}

const unsigned int SCR_WIDTH = 400;
const unsigned int SCR_HEIGHT = 400;

//Crear diferentes shaders para cada una de las figuras 
const char* vertexShaderSrcA = R"glsl(
    #version 460 core
    layout(location = 0) in vec3 aPos;
    void main() {
        gl_Position = vec4(aPos, 1.0);
    }
)glsl";

const char* vertexShaderSrcB = R"glsl(
    #version 460 core
    layout(location = 1) in vec3 aColor;
    void main() {
        gl_Position = vec4(aColor * 0.5, 1.0);
    }
)glsl";

const char* vertexShaderSrcC = R"glsl(
    #version 460 core
    layout(location = 2) in vec2 aOffset;
    void main() {
        gl_Position = vec4(aOffset, 0.0, 1.0);
    }
)glsl";

const char* fragmentShaderSrc = R"glsl(
    #version 460 core
    out vec4 FragColor;
    void main() {
        FragColor = vec4(1.0, 0.5, 0.2, 1.0);
    }
)glsl";

//Las variables
unsigned int VAO, VBO;
unsigned int shaderProgramA, shaderProgramB, shaderProgramC;

unsigned int buildShaderProgram(const char* vertexShaderSrc) {
	int success;
	char log[512];

	unsigned int vs = glCreateShader(GL_VERTEX_SHADER);
	glShaderSource(vs, 1, &vertexShaderSrc, nullptr);
	glCompileShader(vs);
	glGetShaderiv(vs, GL_COMPILE_STATUS, &success);
	if (!success) {
		glGetShaderInfoLog(vs, 512, nullptr, log);
		std::cerr << log << "\n";
	}

	unsigned int fs = glCreateShader(GL_FRAGMENT_SHADER);
	glShaderSource(fs, 1, &fragmentShaderSrc, nullptr);
	glCompileShader(fs);
	glGetShaderiv(fs, GL_COMPILE_STATUS, &success);
	if (!success) {
		glGetShaderInfoLog(fs, 512, nullptr, log);
		std::cerr << log << "\n";
	}

	unsigned int prog = glCreateProgram();
	glAttachShader(prog, vs);
	glAttachShader(prog, fs);
	glLinkProgram(prog);
	glGetProgramiv(prog, GL_LINK_STATUS, &success);
	if (!success) {
		glGetProgramInfoLog(prog, 512, nullptr, log);
		std::cerr << log << "\n";
	}

	glDeleteShader(vs);
	glDeleteShader(fs);
	return prog;
}

//Va a crear 3 triángulos diferentes

void setupTriangle() {
	float vertices[] = {
		-1.0f, -1.0f, 0.0f,   0.0f, 0.0f, 0.0f,   0.1f, 0.5f,
		 0.0f, -1.0f, 0.0f,   1.0f, 0.0f, 0.0f,   0.2f, 0.5f,
		-0.5f, -0.5f, 0.0f,   0.5f, 0.5f, 0.0f,   0.15f, 0.75f,
	};

	glGenVertexArrays(1, &VAO);
	glGenBuffers(1, &VBO);

	glBindVertexArray(VAO);
	glBindBuffer(GL_ARRAY_BUFFER, VBO);
	glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);

	glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 8 * sizeof(float), (void*)(0));
	glEnableVertexAttribArray(0);

	glVertexAttribPointer(1, 3, GL_FLOAT, GL_FALSE, 8 * sizeof(float), (void*)(3 * sizeof(float)));
	glEnableVertexAttribArray(1);

	glVertexAttribPointer(2, 2, GL_FLOAT, GL_FALSE, 8 * sizeof(float), (void*)(6 * sizeof(float)));
	glEnableVertexAttribArray(2);

	glBindVertexArray(0);
}

int main() {
	if (!glfwInit()) return -1;
	glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 4);
	glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 6);
	glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

	GLFWwindow* window = glfwCreateWindow(SCR_WIDTH, SCR_HEIGHT, "Ventana", nullptr, nullptr);
	if (!window) {
		glfwTerminate();
		return -1;
	}

	glfwMakeContextCurrent(window);
	glfwSetFramebufferSizeCallback(window, framebuffer_size_callback);
	if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress)) return -1;
	glfwSwapInterval(1);

	shaderProgramA = buildShaderProgram(vertexShaderSrcA);
	shaderProgramB = buildShaderProgram(vertexShaderSrcB);
	shaderProgramC = buildShaderProgram(vertexShaderSrcC);

	setupTriangle();

	int bufferWidth, bufferHeight;
	glfwGetFramebufferSize(window, &bufferWidth, &bufferHeight);
	glViewport(0, 0, bufferWidth, bufferHeight);

	while (!glfwWindowShouldClose(window)) {
		glfwPollEvents();
		processInput(window);

		glClearColor(0.2f, 0.3f, 0.3f, 1.0f);
		glClear(GL_COLOR_BUFFER_BIT);

		glBindVertexArray(VAO);

		glUseProgram(shaderProgramA);
		glEnableVertexAttribArray(0);
		glDisableVertexAttribArray(1);
		glDisableVertexAttribArray(2);
		glDrawArrays(GL_TRIANGLES, 0, 3);

		glUseProgram(shaderProgramB);
		glDisableVertexAttribArray(0);
		glEnableVertexAttribArray(1);
		glDisableVertexAttribArray(2);
		glDrawArrays(GL_TRIANGLES, 0, 3);

		glUseProgram(shaderProgramC);
		glDisableVertexAttribArray(0);
		glDisableVertexAttribArray(1);
		glEnableVertexAttribArray(2);
		glDrawArrays(GL_TRIANGLES, 0, 3);

		glfwSwapBuffers(window);
	}

	glDeleteVertexArrays(1, &VAO);
	glDeleteBuffers(1, &VBO);
	glDeleteProgram(shaderProgramA);
	glDeleteProgram(shaderProgramB);
	glDeleteProgram(shaderProgramC);

	glfwDestroyWindow(window);
	glfwTerminate();
	return 0;
}
```

**Resultado**
<img width="890" height="679" alt="image" src="https://github.com/user-attachments/assets/b1dd8f48-eab4-4ec4-b1c0-23fc11321767" />




---

##Actividad 05

**1. En esta actividad vas a modificar el ejemplo del triángulo simple para que sea interactivo. La idea es que puedas cambiar el color del triángulo y su posición en la pantalla pasando información desde el código C++ a los shaders.**

```c++
#include <iostream>
#include <glad/glad.h>
#include <GLFW/glfw3.h>


// Callback: ajusta el viewport cuando cambie el tamaño de la ventana
void framebuffer_size_callback(GLFWwindow* window, int width, int height) {
	glViewport(0, 0, width, height);
}

// Procesa entrada simple: cierra con ESC
void processInput(GLFWwindow* window) {
	if (glfwGetKey(window, GLFW_KEY_ESCAPE) == GLFW_PRESS)
		glfwSetWindowShouldClose(window, true);
}

// Tamaño de las ventanas
const unsigned int SCR_WIDTH = 400;
const unsigned int SCR_HEIGHT = 400;

// Fuentes de los shaders
const char* vertexShaderSrc = R"glsl(
#version 460 core

layout(location = 0) in vec3 aPos;
uniform vec2 offset;

void main() {
    vec3 newPos = aPos;
    newPos.x += offset.x;
    newPos.y += offset.y;
    gl_Position = vec4(newPos, 1.0);
}
)glsl";

const char* fragmentShaderSrc = R"glsl(
	#version 460 core

	out vec4 FragColor;
	uniform vec4 ourColor;

	void main() {
		FragColor = ourColor;
	}
)glsl";

// IDs globales
unsigned int VAO, VBO;
unsigned int shaderProg;

// Compila y linkea un programa de shaders, retorna su ID
unsigned int buildShaderProgram() {
	int success;
	char log[512];

	unsigned int vs = glCreateShader(GL_VERTEX_SHADER);
	glShaderSource(vs, 1, &vertexShaderSrc, nullptr);
	glCompileShader(vs);
	glGetShaderiv(vs, GL_COMPILE_STATUS, &success);
	if (!success) {
		glGetShaderInfoLog(vs, 512, nullptr, log);
		std::cerr << "ERROR VERTEX SHADER:\n" << log << "\n";
	}

	unsigned int fs = glCreateShader(GL_FRAGMENT_SHADER);
	glShaderSource(fs, 1, &fragmentShaderSrc, nullptr);
	glCompileShader(fs);
	glGetShaderiv(fs, GL_COMPILE_STATUS, &success);
	if (!success) {
		glGetShaderInfoLog(fs, 512, nullptr, log);
		std::cerr << "ERROR FRAGMENT SHADER:\n" << log << "\n";
	}

	unsigned int prog = glCreateProgram();
	glAttachShader(prog, vs);
	glAttachShader(prog, fs);
	glLinkProgram(prog);
	glGetProgramiv(prog, GL_LINK_STATUS, &success);
	if (!success) {
		glGetProgramInfoLog(prog, 512, nullptr, log);
		std::cerr << "ERROR LINKING PROGRAM:\n" << log << "\n";
	}

	glDeleteShader(vs);
	glDeleteShader(fs);
	return prog;
}

// Crea un VAO/VBO con los datos de un triángulo
void setupTriangle() {
	float vertices[] = {
		-0.5f, -0.5f, 0.0f,
		 0.5f, -0.5f, 0.0f,
		 0.0f,  0.5f, 0.0f
	};
	glGenVertexArrays(1, &VAO);
	glGenBuffers(1, &VBO);

	glBindVertexArray(VAO);


	glBindBuffer(GL_ARRAY_BUFFER, VBO);
	glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
	glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0);
	glEnableVertexAttribArray(0);
	glBindVertexArray(0);
}


int main()
{
	// 1) Inicializar GLFW
	if (!glfwInit()) {
		std::cerr << "Fallo al inicializar GLFW\n";
		return -1;
	}
	glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 4);
	glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 6);
	glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

	// 2) Crear ventana
	GLFWwindow* mainWindow = glfwCreateWindow(SCR_WIDTH, SCR_HEIGHT, "Ventana", nullptr, nullptr);
	if (!mainWindow) {
		std::cerr << "Error creando ventana1\n";
		glfwTerminate();
		return -1;
	}

	// 3) Lee el tamaño del framebuffer
	int bufferWidth, bufferHeight;
	glfwGetFramebufferSize(mainWindow, &bufferWidth, &bufferHeight);
	
	// 4) Callbacks 
	glfwSetFramebufferSizeCallback(mainWindow, framebuffer_size_callback);


	// 5) Cargar GLAD y recursos en contexto de window1
	glfwMakeContextCurrent(mainWindow);

	if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress)) {
		std::cerr << "Fallo al cargar GLAD (contexto1)\n";
		return -1;
	}

	// 6) Habilita el V-Sync
	glfwSwapInterval(1);

	// 7) Compila y linkea shaders
	shaderProg = buildShaderProgram();

	// 8) Genera el contenido a mostrar
	setupTriangle();

	// 9) Configura el viewport
	glViewport(0, 0, bufferWidth, bufferHeight);

	glUseProgram(shaderProg);
	int offsetLocation = glGetUniformLocation(shaderProg, "offset");
	int colorLocation = glGetUniformLocation(shaderProg, "ourColor");

	// 10) Loop principal
	while (!glfwWindowShouldClose(mainWindow))
	{
		// 11) Manejo de eventos
		glfwPollEvents();

	
		// 12) Procesa la entrada
		processInput(mainWindow);

		// 13) Configura el color de fondo y limpia el framebuffer
		glClearColor(0.2f, 0.3f, 0.3f, 1.0f);
		glClear(GL_COLOR_BUFFER_BIT);
		
		// 14) Indica a OpenGL que use el shader program
		glUseProgram(shaderProg);

		// Dibuja el triángulo
		double xpos, ypos;
		glfwGetCursorPos(mainWindow, &xpos, &ypos);

		// Normalizo las coordenadas del mouse
		float x = (float)xpos / (float)SCR_WIDTH;
		x < 0 ? x = 0 : x;
		x > 1 ? x = 1 : x;

		float y = (float)ypos / (float)SCR_HEIGHT;
		y < 0 ? y = 0 : y;
		y > 1 ? y = 1 : y;

		// Envio el color y la posición del triángulo
		float color[] = { x, y, 0.0f, 1.0f };
		glUniform4f(colorLocation, x, y, 0.0f, 1.0f);

		// Envio el offset del triángulo normalizado a NDC
		glUniform2f(offsetLocation, x * 2 - 1, 1 - y * 2);


		// 15) Activa el VAO y dibuja el triángulo
		glBindVertexArray(VAO);
		glDrawArrays(GL_TRIANGLES, 0, 3);

		// 16) Intercambia buffers y muestra el contenido
		glfwSwapBuffers(mainWindow);
	}

	// 17) Limpieza
	glfwMakeContextCurrent(mainWindow);
	glDeleteVertexArrays(1, &VAO);
	glDeleteBuffers(1, &VBO);
	glDeleteProgram(shaderProg);

	glfwDestroyWindow(mainWindow);
	glfwTerminate();
	return 0;
}
```

**2. Incluye una captura de pantalla del triángulo interactivo funcionando en tu máquina.**

<img width="891" height="687" alt="image" src="https://github.com/user-attachments/assets/82c4cc30-c856-49c4-8e32-a45940da13e9" />

<img width="915" height="694" alt="image" src="https://github.com/user-attachments/assets/80fa6f99-85f1-40cc-a34e-3eb16db1ac5e" />

<img width="907" height="690" alt="image" src="https://github.com/user-attachments/assets/3c876f59-6d01-46a9-9f14-32d7f267f1fa" />



**3. Explica el proceso de normalización de las coordenadas del mouse y cómo se relaciona con el sistema de coordenadas de OpenGL.**

Luego de leer La normalización de coordenadas del mouse es que según la posición del mouse en la ventana se le asigna unos valores en x y en y, así es como el programa sabe en qué parte está el mouse. La normalización es para obtener números entre 0 y 1 entonces se convierte dividiendo la coordenadas x y y del mouse por el ancho y la altura de la pantalla respectivamente.

**4. Explica el proceso de normalización a coordenadas de dispositivo (NDC) y cómo se relaciona con el sistema de coordenadas de OpenGL.**

OpenGL usa números entre -1 y 1 entonces se usa una fórmula para que OpenGL pueda entender los valores y dibujarlos. 

c++
```
// Envio el offset del triángulo normalizado a NDC
glUniform2f(offsetLocation, x * 2 - 1, 1 - y * 2);
```

---

## Actividad 06

**Tu misión es modificar el ejemplo del triángulo simple (puedes partir del resultado de la Actividad 05 o del original) para que su color cambie automáticamente a lo largo del tiempo, creando un efecto pulsante o cíclico.**

**1. Describe brevemente los cambios que realizaste en el código C++ (dónde obtienes el tiempo, cómo y dónde actualizas el uniform).**
**2. Pega el código modificado de tu fragment shader.**
**3. Explica cómo usaste la función de tiempo (sin, cos, u otra) para lograr el efecto de cambio de color cíclico. ¿Qué rango de valores produce tu cálculo y cómo afecta eso al color final?**
**4. Incluye una captura de pantalla o UN ENLACE a un video mostrando el resultado del triángulo con color cambiante.**
**5. Reflexión: ¿Qué otros efectos visuales simples podrías lograr usando el tiempo como uniform? Piensa en la posición, el tamaño o la rotación (aunque no hemos visto rotaciones formalmente, ¡intuitivamente podrías intentarlo!). Anota al menos una idea.

---

Rúbrica
5: realice las 6 actividades completas y la autoevaluación.
4: realicé 5 actividades completas y la autoevaluación.
3: realicé 4 actividades completas y la autoevaluación.
2: realicé 3 actividades completas y la autoevaluación.
1: realicé 2 actividades completas y la autoevaluación.
0.5: realicé 1 actividad completa y la autoevaluación.
0: no realicé ninguna actividad o no realicé la autoevaluación.

---

## Nota: 4.0

-Actividad 01: Completa (0.5)
-Actividad 02: Completa (0.5)
-Actividad 03: Completa (1.0)
-Actividad 04: Completa (1.0)
-Actividad 05: Completa (1.0)
-Actividad 06: Incompleta (0.0)


