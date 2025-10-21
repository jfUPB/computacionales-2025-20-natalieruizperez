# Bitácora de aprendizaje de la unidad 8



---

## Actividad 01

**1. Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto?**

Al dar click el círculo se va a detener porque al dar click se está calculando un nuevo tamaño para la bola y mientras que el hilo principal de openframeworks hace el cálculo ya se no se puede mover. Al darle esc la ventana no se va a cerrar ahí mismo si el hilo está ocupado haciendo cálculos.

**2. Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto? Observa que el programa ahora no se congela, pero el círculo no cambia de tamaño inmediatamente. ¿Por qué crees que sucede esto? ¿Qué es lo que está pasando?**


Para arreglarlo es el mismo caso pero ahora cuando se da click se recibe el pedido y ocurre hasta que el hilo termine. La aplicación sigue funcionando y después de un rato de dar click se actualiza gracias a que ya hay responsividad.

**3. En tus propias palabras, explica la diferencia entre concurrencia y paralelismo. ¿Por qué es importante entender esta diferencia al trabajar con hilos?**

La ejecución es paralela cuando se le puede asignar a cada uno un core y estamos haciendo todo al mismo tiempo, en cambio la concurrencia es hacer un poco de cada cosa pero de forma muy rápida. 

---
## Actividad 02
**1. Analiza de nuevo el código de la actividad anterior. ¿En qué partes del código se está protegiendo el acceso a la variable circleSize?**


Cada que se apreta R va a ejecutarse el experimento. Cuando se le quita el candado el contador ya no llega hasta el valor esperado. Es un error de concurrencia dado que . Cada quese corre el experimento el programa hace lo mismo en cada ejecución pero nunca da el mismo resultado y se queda en los rangos de un millón. Aquí se demora menos porque 

**2. Según lo que te he venido comentando, los hilos te permiten ejecutar tareas en paralelo; sin embargo, piensa qué ocurre con el paralelismo cuando se sincroniza el acceso a un recurso compartido. ¿Qué ocurre con el rendimiento del programa? ¿Es posible que el rendimiento se vea afectado por el uso de mutex? ¿Por qué?**

**3. Ejecuta el código y observa el resultado. ¿Qué ocurre si cambias el valor de la variable useLock? ¿Por qué crees que ocurre esto?**

**4. Explica en tus propias palabras ¿Cómo puede presentarse la condición de carrera en este caso? ¿Qué es lo que está pasando? Te pido que propongas un ejemplo.**

Diferenciar que es un hilo y un proceso (diferencia) y también cuando se habla de concurrencia y paralelismo.

---
## Actividad 03

**1. Ejecuta el código y observa el resultado.**
Al apretar espacio se demora más tiempo a medida que aumento las iteracaciones. Se observa una especie de . En la versión paralela aunque este en muchas iteraciones es más estable y más rápido al usar los 16 hilos.

**Analiza el código y estudia detenidamente su funcionamiento. En la fase de aplicación tendrás que retomar este código para resolver un reto.**

Para cada pixel hay que hacer el cálculo de lalgortimo y tomar cada uno y hacer un algoitmo interacti

**Experimenta modificando, PERO, no olvides cómo investigamos en este curso: Realiza cambios pequeños y específicos. Lanza una hipótesis sobre lo que crees que va a pasar. Ejecuta el código y observa lo que ocurre. ¿Tu hipótesis era correcta? ¿Por qué crees que ocurre esto? Te dejo una idea para comenzar a experimentar: ¿Qué ocurre si cambias el número de hilos? ¿Por qué crees que ocurre esto?**

## Actividad 04 

**Observa ambos códigos y responde a las siguientes preguntas:**

Para la versión de un solo hilo que es altamente paralelizable a medida que se crean agentes los fps se van colapsando, cuando ya son muchos los fps caen. Eso es porque el algoritmo cálcula como se comporta con respecto a las demás y eso lo tiene que hacer para cada una. En el segundo código que trabaja con más hilos al subir las criaturas pero como no es altamente paralelizable no hay mucha ganancia. 

**1. ¿Cuál es la estructura de datos principal que contiene la información de todos los boids y que es accedida por múltiples hilos (el hilo principal para dibujar, el hilo trabajador para actualizar)?**

**2. Observa la función Flock::threadedFunction() donde el hilo trabajador calcula el movimiento. ¿Qué operaciones realizan sobre el vector de boids compartido?**

**3. Observa la función ofApp::draw(). ¿Qué operación realiza sobre el vector compartido?**

**4. Observa Flock::addBoid() y ofApp::mouseDragged(). ¿Qué operación realizan?**

**5. Describe un escenario específico y concreto donde la falta de sincronización podría causar un problema. Por ejemplo: “El Hilo X está recorriendo el vector para calcular la separación (leyendo posiciones). Al mismo tiempo, el Hilo Y (llamado desde mouseDragged) intenta añadir un nuevo boid al final del vector. ¿Qué podría pasarle al iterador del Hilo X o al tamaño del vector que está usando?”
Localiza todas las llamadas a lock() y unlock() dentro de la clase Flock (o donde se acceda al vector compartido).

Justificación: para uno de los escenarios problemáticos que describiste arriba, explica cómo las llamadas a lock()/unlock() en las secciones de código relevantes evitan que ocurra ese problema específico.

---
## Actividad 05
Hay que calcular una imagen de 1024x768 que es demorado hacerlo pero se están usando 16 hilos y es por eso que ya se puede tener una aplicación en tie,po real. La ventaja de tener hilos es que sirve en tiempo real entonces podría estarse controlando a través de música por ejemplo.

Pega la parte clave de tu función modificada que calcula el píxel para el conjunto de Julia. Recuerda utilizar un bloque cpp.
Muestra cómo mapeaste la posición del mouse a la constante k.
Describe brevemente cómo reutilizaste la estructura de hilos de la versión Mandelbrot. ¿Tuviste que cambiar mucho esa parte?
¿Cómo te aseguraste de que la imagen se recalculara cuando el mouse se movía?
Incluye al menos dos capturas de pantalla que muestren diferentes fractales de Julia generados al mover el mouse en tu aplicación.
¿Encontraste algún desafío particular al implementar la interacción o modificar el cálculo?

---
Notas de clase: Un proceso es un programa. La concurrencia es diferente al paralelismo. La ejecución es paralela cuando se le puede asignar a cada uno un core y estamos haciendo todo al mismo tiempo, en cambio la concurrencia es hacer un poco de cada cosa pero de forma muy rápida. La responsividad de la aplicación.

---

Rúbrica

---
## Nota: 

-Actividad 01: Completa (1.0)

Aunque los locks aseguran la correctitud, ¿Puedes intuir por qué tener muchos hilos esperando para adquirir un lock sobre el mismo vector (alta contención) podría limitar el beneficio de rendimiento del paralelismo en este caso? Justifica tu respuesta.
