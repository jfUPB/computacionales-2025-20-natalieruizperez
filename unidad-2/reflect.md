# Unidad 2


## 🤔 Fase: Reflect

### Actividad 05

#### Parte 1: recuperación de conocimiento (retrieval practice)

**1. Describe con tus palabras las tres fases del ciclo Fetch-Decode-Execute. ¿Qué rol juega el Program Counter (PC) en este ciclo?**

El program counter juega el programa de mostrar cuál línea es la que se va a ejecutar, sirve para saber en qué parte del código vamos cuando lo estamos probando. La fase fetch consiste en buscar, la decode en decodificar que sería procesar la información y la execute es para ejecutar la acción.

**2. ¿Cuál es la diferencia fundamental entre una instrucción-A (que empieza con @) y una instrucción-C (que involucra D, M, A, etc.) en el lenguaje ensamblador de Hack? Da un ejemplo de cada una.**

La instrucción A es una que podemos modificar constantemente y la única forma de asignarle valor a las variables, si queremos asignarle a D un número no se puede hacer directamente, solo si decimos que D=A. Otra sería cuando quiero guardar algo en la memoria que hago M=D, está instrucción tiene en cuenta el valor de A que es en donde se va a almacenar el valor de D.

**3. Explica la función de los siguientes componentes del computador Hack: el registro D, el registro A y la ALU.**

ALU sirve para hacer operaciones como por ejemplo D=D-A, también los saltos. El registro A se puede cambiar para crear valores diferentes y también para acceder a una dirección específica de memoria. En cambio la D se usa temporalmente para cálculos.

**4. ¿Cómo se implementa un salto condicional en Hack? Describe un ejemplo (p. ej., saltar si el valor de D es mayor que cero).**

Un salto condicional en hack se hace con D=D-A y lueg poniendo la condición como por ejemplo D;JGT.

**5. ¿Cómo se implementa un loop en el computador Hack? Describe un ejemplo (p. ej., un loop que decremente un valor hasta que llegue a cero).**

Primero se pone una etiqueta para saber donde empieza el loop y al final se le asigna a A ese valor para qu vaya a la etiqueta si sucede un condicional.

**6. ¿Cuál es la diferencia entre la instrucción D=M y la instrucción M=D?**

M=D hace que se guarde el valor de D en la dirección de la memoria de A, mientras que D=M toma el valor que está en la dirección de la memoria de A.   

**Describe brevemente qué se necesita para leer un valor del teclado (KBD) y para “pintar” un pixel en la pantalla (SCREEN).**

Para leer un valor de teclado KBD es necesario poner @KBD y luego guardarlo diciendo D=M. Ahora para pintar un pixel en screen sería poner @screen y luego M=1.

#### Parte 2: reflexión sobre tu proceso (metacognición)

**1. ¿Cuál fue el concepto o actividad más desafiante de esta unidad para ti y por qué?**

La última me pareció excesivamente difícil, era muy manual y había que hacer un código largo ya que no hay una fomra sencilla de programar lenguaje ensamblado. En general me pareció muy confuso.

**2. La metodología de “predecir, ejecutar, observar y reflexionar” fue central en nuestras actividades. ¿En qué momento esta metodología te resultó más útil para entender algo que no tenías claro?**

Esa metodología me ha servido bastante a lo largo del curso pero en la última actividad seguir esta metodología me pareció muy complicado porque era un proceso muy largo y por tener tantos códigos en la pantalla me perdía y no sabía qué estaba haciendo. Más que servir para reflexionar me pareció que creaba desorden-

**3. Describe un momento “¡Aha!” que hayas tenido durante estas dos semanas. ¿Qué estabas haciendo cuando ocurrió?**


**4. Pensando en la próxima unidad, ¿Qué harás diferente en tu proceso de estudio para aprender de manera más efectiva?**
Quizás no predecir tanto en actividades en las que haya que hacer un código muy largo porque personalmente ese proceso no me sirvió en esos casos específicos.

### Actividad 07 - Feedback
**1. Continuar: ¿Qué aspecto de las actividades, las explicaciones o la dinámica de la clase te ha resultado más útil o te ha gustado más y debería seguir haciendo?**
Me gustó que en clase

**2. Dejar de hacer: ¿Qué aspecto de la unidad te ha resultado confuso, poco útil o frustrante? ¿Hay algo que crees que debería eliminar o cambiar drásticamente?**

**3. Empezar a hacer: ¿Qué te habría gustado que hiciéramos que no hicimos? ¿Tienes alguna idea para una actividad o un recurso que podría mejorar el aprendizaje en la próxima unidad?**

**4. Ritmo y Dificultad: en una escala del 1 (muy fácil/lento) al 5 (muy difícil/rápido), ¿Cómo calificarías el ritmo y la dificultad general de esta unidad? ¿Por qué?**
Le doy un 5, la última actividad me pareció muy difícil y con la metodología se me complicó aún más.

***5. Comentario Adicional: ¿Hay algo más que te gustaría compartir sobre tu experiencia de aprendizaje en esta unidad?**
