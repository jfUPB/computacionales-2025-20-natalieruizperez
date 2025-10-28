# Bitácora de aprendizaje de la unidad 8



---

## Actividad 01

**1. Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto?**

Veo un círculo negro que va del lado izquierdo al derecho en un fondo blanco.

<img width="393" height="423" alt="image" src="https://github.com/user-attachments/assets/659ca0d4-fe80-478c-b74d-a79cbf9de54c" />

Al leer el código por encima espero que haya una forma de cambiarle el tamaño al círculo.

Veo que al dar click el círculo se deti8ene el círculo, creo que esto sucede porque se está calculando un nuevo tamaño para la bola y mientras que el hilo principal de openframeworks hace el cálculo ya se no se puede mover. Al darle esc la ventana no se va a cerrar ahí mismo si el hilo está ocupado haciendo cálculos.

**2. Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto? Observa que el programa ahora no se congela, pero el círculo no cambia de tamaño inmediatamente. ¿Por qué crees que sucede esto? ¿Qué es lo que está pasando?**

<img width="756" height="398" alt="image" src="https://github.com/user-attachments/assets/f95f12c1-282c-4aa3-9cab-e63eb5ddc8f1" />

Esta vez hay textos explicativos de que está sucediendo mientras se ejecuta la aplicación, también es el mismo círculo del ejercicio anterior solo que está vez no se detiene el programa inmediatamente al darle click derecho, si no que continua ejecutándose en lo que calcula el tamaño. Esto hace ya no parezca un error del programa y me parece que es una forma efectiva de hacer tiempo para que los hilos calculen el nuevo tamaño. Creo que sucede esto porque después de un rato de dar click se actualiza gracias a que ya hay responsividad.

**3. En tus propias palabras, explica la diferencia entre concurrencia y paralelismo. ¿Por qué es importante entender esta diferencia al trabajar con hilos?**

La ejecución es paralela cuando se le puede asignar a cada uno un core y estamos haciendo todo al mismo tiempo, en cambio la concurrencia es hacer un poco de cada cosa pero de forma muy rápida, como volver a la tarea de formas reiteradas. 

---
## Actividad 02
**1. Analiza de nuevo el código de la actividad anterior. ¿En qué partes del código se está protegiendo el acceso a la variable circleSize?**

Creo que se está protegiendo en la función draw() y heavyComputation() ya que hace algo similar a lo que se explicaba con el concepto de mutex que es que se bloquea y después se desbñpquea.

**ofApp.cpp

c++
```
void ofApp::draw() {

	ofBackground(220);
	ofSetColor(0);
	lock();
	ofDrawCircle(x, ofGetHeight() / 2, circleSize);
	unlock();
	x = fmod(x + speed, ofGetWidth());
}


void ofApp::heavyComputation() {
	double result = 0;
	for (int j = 0; j < 1000000000; ++j) {
		result += sqrt(j);
	}
	lock();
	ofSeedRandom();
	circleSize = ofRandom(20, 70);
	unlock();
	std::cout << "Circle size: " << circleSize << std::endl;
}
```

**2. Según lo que te he venido comentando, los hilos te permiten ejecutar tareas en paralelo; sin embargo, piensa qué ocurre con el paralelismo cuando se sincroniza el acceso a un recurso compartido. ¿Qué ocurre con el rendimiento del programa? ¿Es posible que el rendimiento se vea afectado por el uso de mutex? ¿Por qué?**

En el paralelismo cuando se sincroniza el acceso a un recurso compartido puede causar que accedan al mismo tiempo a ese recurso y lo modifiquen en el orden incorrecto causando que el rendimiento del programa sea inesperado. Creo que el uso del mutex favorece al rendimiento del programa ya que evita que ocurran errores y haya una sincronización correcta.

**3. Ejecuta el código y observa el resultado. ¿Qué ocurre si cambias el valor de la variable useLock? ¿Por qué crees que ocurre esto?**

<img width="1011" height="758" alt="image" src="https://github.com/user-attachments/assets/62c5d3ea-9ae0-413d-bd67-ddc24a8fda08" />

Al ejecutar el código veo que cada vez que apreto r con el candado el contador llega al resultado esperado. Si cambio el valor de la variable useLock a falso veo que ya no llega hasta el valor esperado si no que oscila entre valores de un millon y dos millones y medios. Creo que ocurre porque los hilos están intentando modificar el contador al mismo tiempo

<img width="1018" height="759" alt="image" src="https://github.com/user-attachments/assets/5c5135f0-896a-4aab-a60e-fdd87af8f78f" />

**4. Explica en tus propias palabras ¿Cómo puede presentarse la condición de carrera en este caso? ¿Qué es lo que está pasando? Te pido que propongas un ejemplo.**

 La condición de carrera en este caso se presenta cada vez que se presiona r para inicializar el contador, esto sucede porque diferentes hilos acceden a la variable y la modifican incrementando el valor sin algún orden específico. Se puede observar por ejemplo cada que se corre el experimento el programa hace lo mismo en cada ejecución pero nunca da el mismo resultado y se queda en los unos rangos específicos.


---
## Actividad 03

**1. Ejecuta el código y observa el resultado.**
En el secuencial observo que al apretar espacio se demora más tiempo a medida que aumenta las iteracaciones. En cambio, en la versión paralela aunque este en muchas iteraciones es más estable y más rápido al usar los 16 hilos.

Ambas capturas de pantalla fueron tomadas mientras que apretaba la tecla de espacio muchas veces.

**Secuencial**
<img width="1016" height="761" alt="image" src="https://github.com/user-attachments/assets/aa7e44f6-c717-47df-9cd7-1f874d7faf01" />

**Paralela**
<img width="1012" height="758" alt="image" src="https://github.com/user-attachments/assets/dc80f1fa-4022-4a77-978a-5168a47952a5" />


**Analiza el código y estudia detenidamente su funcionamiento. En la fase de aplicación tendrás que retomar este código para resolver un reto.**

Para cada pixel hay que hacer el cálculo de algoritmo.

**Experimenta modificando, PERO, no olvides cómo investigamos en este curso: Realiza cambios pequeños y específicos. Lanza una hipótesis sobre lo que crees que va a pasar. Ejecuta el código y observa lo que ocurre. ¿Tu hipótesis era correcta? ¿Por qué crees que ocurre esto? Te dejo una idea para comenzar a experimentar: ¿Qué ocurre si cambias el número de hilos? ¿Por qué crees que ocurre esto?**

Creo que si cambio el número de hilos aumentándolos los fps no bajarán tanto dado que habrán varios trabajando en paralelo para llevar a cabo ese proceso, en cambio si disminuyo el número de hilos considero que la aplicación podría demorarse muchísimo más en lanzar la imagen.

**1 hilo**
<img width="1012" height="758" alt="image" src="https://github.com/user-attachments/assets/6de1c704-161b-4fad-9158-799e7deee983" />

**8 hilos**
<img width="1017" height="756" alt="image" src="https://github.com/user-attachments/assets/abddd24c-742c-4ee6-9f11-a5a0f4e173cf" />

**16 hilos**
<img width="1009" height="760" alt="image" src="https://github.com/user-attachments/assets/2e03c4c9-90ab-4692-ab0d-80d38313f7f4" />

**32 hilos**
<img width="1015" height="766" alt="image" src="https://github.com/user-attachments/assets/dd0af58d-5141-4fc8-842b-a73d96e12984" />


**100 hilos**
<img width="1012" height="758" alt="image" src="https://github.com/user-attachments/assets/45bc4925-17d1-48ac-986f-50bf1747933e" />

Al observar los resultados obtenidos me doy cuenta de que efectivamente al tener un solo hilo tarda más en producir la imagen. El de 32 hilos es mucho más rápido que el del 100 hilos esto es porque a los 100 hilos ocurre concurrencia porque el computador no puede llevar esas tareas en paralelo. 32 hilos que es la capacidad máxima que puede generar el computador para que ocurra paralelismo es por esto que aquí es donde hay menor tiempo.

---
## Actividad 04 

**Flocking sin hilos**

<img width="1016" height="800" alt="image" src="https://github.com/user-attachments/assets/fd39a5bf-98c3-4a6b-ab5d-f3991c2d0af4" />

A medida que aumenta la cantidad de boids los fps bajan y el programa se pone mas lento.

**Flocking con hilos**

<img width="1021" height="793" alt="image" src="https://github.com/user-attachments/assets/bab8d0c7-5193-4847-a697-715dc166df7b" />

Tienen una cantidad similar de boids pero el programa, corre a mas fps y se siente un poco mas fluidos pero no veo mucha diferencia.

**Observa ambos códigos y responde a las siguientes preguntas:**

Nota de clase: Para la versión de un solo hilo que es altamente paralelizable a medida que se crean agentes los fps se van colapsando, cuando ya son muchos los fps caen. Eso es porque el algoritmo cálcula como se comporta con respecto a las demás y eso lo tiene que hacer para cada una. En el segundo código que trabaja con más hilos al subir las criaturas pero como no es altamente paralelizable no hay mucha ganancia. 

**1. ¿Cuál es la estructura de datos principal que contiene la información de todos los boids y que es accedida por múltiples hilos (el hilo principal para dibujar, el hilo trabajador para actualizar)?**

La estructura de datos principal que contiene la información de todos los boids y que es accedida por múltiples hilos es la clase flock : public ofThread que llama a varias funciones y también esta std::vector<Boid> boids; que es donde se guardan.

**2. Observa la función Flock::threadedFunction() donde el hilo trabajador calcula el movimiento. ¿Qué operaciones realizan sobre el vector de boids compartido?**

El vector de boids compartidos realiza varias operaciones entre ellas el sistema de lock para que los hilos no accedan al mismo tiempo para que así no ocurra una condición de carrera. También hay un puntero que recorre los voids y sleep que es para que haya un tiempo entre acción y acción, evitando que se sobrelapen.

**3. Observa la función ofApp::draw(). ¿Qué operación realiza sobre el vector compartido?**

Veo que dibuja el fondo, y el vector compartido llama a la función draw que cuenta con varios aspectos de los voids como el color, posición, rotación, y también hace 3 operaciones diferentes que asumo que se encargan de que haya separación, alineación y cohesión en el sistema.

**4. Observa Flock::addBoid() y ofApp::mouseDragged(). ¿Qué operación realizan?**

addBoid se encarga de crear un nuevo ente el el programa, también cuenta con unas funciones de lock y unlock y mouse dragged hace que se creen esos boids en la posición del mouse a medida que es arrastrado.

**5. Describe un escenario específico y concreto donde la falta de sincronización podría causar un problema. Por ejemplo: “El Hilo X está recorriendo el vector para calcular la separación (leyendo posiciones). Al mismo tiempo, el Hilo Y (llamado desde mouseDragged) intenta añadir un nuevo boid al final del vector. ¿Qué podría pasarle al iterador del Hilo X o al tamaño del vector que está usando?”
Localiza todas las llamadas a lock() y unlock() dentro de la clase Flock (o donde se acceda al vector compartido).

En ese ejemplo en el que un hilo recorre el vector para calcular la separación e intenta añadir un vector al final podría causar crasheos, la solución sería poner el lock en las funciones donde se agregan los boids, se dibujan y de donde se manejan todos los threads, al final desbloquearlos para que funcionen correctamente y se puedan acceder una vez ya haya terminado de usarlo algun hilo.

Justificación: para uno de los escenarios problemáticos que describiste arriba, explica cómo las llamadas a lock()/unlock() en las secciones de código relevantes evitan que ocurra ese problema específico.

**¿Qué pasaría si tuviéramos varios hilos que calculan el movimiento de los boids? ¿Cómo podrías implementar esto? ¿Qué problemas crees que podrían surgir? ¿Cómo podrías solucionarlos?**

Si tuvieramos varios hilos que calculan el movimiento de los boids sería necesario añadir lock() y unlock() para que no hayan crasheos y tampoco errores condiciones de carrera donde los hilos acceden al movimiento de los voids y los calculan simultáneamente haciendo que haya una sobreposición de datos. La solución sería la que mencioné, asegurarse de bloquear y desbloquear  las funciones para que no cambien los calculos ya hechos si no que puedan trabajar en conjunto, es decir que haya paralelismo y concurrencia.

**1. Analiza el código del Flocking sin hilos y el Flocking con hilos. ¿Qué diferencias encuentras? ¿Por qué crees que es importante la sincronización en el segundo caso?**

Al inicio de la actividad había escrito de forma más detallada el análisis de los códigos, creo que es importante la sincronización en el segundo caso porque a pesar de que no hay gran diferencia en cuanto a fps, el programa en el segundo caso se nota más fluido.

**2. ¿Por qué al añadir un nuevo boid la simulación se ralentiza? ¿Qué ocurre si añades muchos boids?**

Esto sucede porque no estamos usando hilos para que procesen la información.

**3. Notaste que la versión con hilos tiene un sleep(5) en el hilo trabajador. ¿Por qué crees que se ha añadido? ¿Qué pasaría si lo eliminamos?**

Esto ya lo había mencionado cuando analicé el código pero creo que el propósito es que haya un tiempo de pausa entre boid y boid para que el sistema pueda "descansar" y no solo eso si no también seguir un orden. Si se elimina ocurrirían errores.

**4. Compara el rendimiento de ambos enfoques. ¿Cuál crees que es más eficiente? ¿Por qué?**

El más eficiente es el segundo porque usa hilos para evitar que se ralentice el sistema.

**5. El uso de lock y unlock en la versión con hilos es crucial para evitar condiciones de carrera. ¿Qué pasaría si no se usaran? ¿Cómo afectaría esto al comportamiento del programa? (No olvides por favor que las condiciones de carrera son difíciles de reproducir, así que no te preocupes si no puedes verlas en acción).**

Si no se usaran el programa se crashearía y afectaría al programa haciendo que los valores se reemplacen unos a otros ya que estarían trabajando los hilos sin seguir un orden específico.

---
## Actividad 05
Hay que calcular una imagen de 1024x768 que es demorado hacerlo pero se están usando 16 hilos y es por eso que ya se puede tener una aplicación en tie,po real. La ventaja de tener hilos es que sirve en tiempo real entonces podría estarse controlando a través de música por ejemplo.

Pega la parte clave de tu función modificada que calcula el píxel para el conjunto de Julia. Recuerda utilizar un bloque cpp.
Muestra cómo mapeaste la posición del mouse a la constante k.
Describe brevemente cómo reutilizaste la estructura de hilos de la versión Mandelbrot. ¿Tuviste que cambiar mucho esa parte?
¿Cómo te aseguraste de que la imagen se recalculara cuando el mouse se movía?
Incluye al menos dos capturas de pantalla que muestren diferentes fractales de Julia generados al mover el mouse en tu aplicación.
¿Encontraste algún desafío particular al implementar la interacción o modificar el cálculo?
Aunque los locks aseguran la correctitud, ¿Puedes intuir por qué tener muchos hilos esperando para adquirir un lock sobre el mismo vector (alta contención) podría limitar el beneficio de rendimiento del paralelismo en este caso? Justifica tu respuesta.

---
Notas de clase: Un proceso es un programa. La concurrencia es diferente al paralelismo. La ejecución es paralela cuando se le puede asignar a cada uno un core y estamos haciendo todo al mismo tiempo, en cambio la concurrencia es hacer un poco de cada cosa pero de forma muy rápida. La responsividad de la aplicación.

---
**Rúbrica**

5: realicé las 5 actividades completas y la autoevaluación.

  4: realicé 4 actividades completas y la autoevaluación.

  3: realicé 3 actividades completas y la autoevaluación.

  2: realicé 2 actividades completas y la autoevaluación.

  1: realicé 1 actividad completa y la autoevaluación.

  0: no realicé ninguna actividad o no realicé la autoevaluación.
---
## Nota: 4.0

-Actividad 01: Completa (1.0)
-Actividad 02: Completa (1.0)
-Actividad 03: Completa (1.0)
-Actividad 04: Completa (1.0)
-Actividad 05: No realizada (0.0)

