# Unidad 1

## 🤔 Fase: Reflect

### Actividad 05
Sin consultar tus apuntes

---
#### Parte 01 : Recuperación de conocimiento (retrieval practice)

##### Describe con tus palabras las tres fases del ciclo Fetch-Decode-Execute. ¿Qué rol juega el Program Counter (PC) en este ciclo?
La primera fase que es buscar es cuando la computadora toma la instrucción que está en la memoria en la dirección que indica el Program Counter (PC). Después se decodifica entonces la instrucción que se sacó se interpreta para entender qué debe hacer la computadora. Finalmente para la parte de ejecutar la computadora realiza la acción de la instrucción. El Program Counter juega un papel importante en el ciclo ya que nos permite saber qué parte del programa se va a ejecutar.

##### ¿Cuál es la diferencia fundamental entre una instrucción-A (que empieza con @) y una instrucción-C (que involucra D, M, A, etc.) en el lenguaje ensamblador de Hack? Da un ejemplo de cada una.
La instrucción que empieza por @ es la que le asigna un valor a A, puede ser un número (@6, lo que quiere decir que A es 6) o una oración (@END, que le da el valor a A de END y sirve para ir a la etiqueta de esa instrucción si se pone un salto).

##### Explica la función de los siguientes componentes del computador Hack: el registro D, el registro A y la ALU.
El registro A es aquel que toma el valor que se le ponga a la hora de escribir @valor, en cambio el registro D no tiene forma de darle un valor dce forma directa, pero si es posible al relacionar a A con D diciendo que D = A. La ALU son las operaciones, creo recordar que significaba Algorithm Logic Unit que vendrían siendo operaciones como suma o resta por ejemplo D = D-A

##### ¿Cómo se implementa un salto condicional en Hack? Describe un ejemplo (p. ej., saltar si el valor de D es mayor que cero).
El salto condicional en el hack se implementa siempre y cuando se cumpla una condición. Por ejemplo si tengo @LOOP cuando D;JGT, es decir que haga un salto cuando D sea mayor o igual que 0, este irá al lugar en dónde puse la etiqueta.

##### ¿Cómo se implementa un loop en el computador Hack? Describe un ejemplo (p. ej., un loop que decremente un valor hasta que llegue a cero).
En un computador Hack se implementa un loop usando etiquetas y saltos. Por ejemplo, para bajar un valor hasta que llegue a cero, primero se guarda el número en un lugar, después se pone una etiqueta en el inicio del loop y pongo un salto que solo se hace si el valor sigue siendo mayor que cero (D; JGT), entonces se repite hasta llegar a 0.

##### ¿Cuál es la diferencia entre la instrucción D=M y la instrucción M=D?
La diferencia entre la instrucción D=M y M=D es que en la primera instrucción se le está dando a D el valor que esté en la posición de la memoria de M, en cambio la segunda hace que la memoria tome el valor de D en la posición correspondiente mencionada.

##### Describe brevemente qué se necesita para leer un valor del teclado (KBD) y para “pintar” un pixel en la pantalla (SCREEN).
Para leer un valor del teclado, se usa @KBD que es 24576, y una etiqueta (KEYPRESSED) que cambia cuando se presiona una tecla. Para pintar un pixel en la pantalla, se usa @SCREEN que es 16384 y después se guarda un valor en la memoria para que se vea el pixel.

--- 
#### Parte 2: Reflexión sobre tu proceso (metacognición)
##### ¿Cuál fue el concepto o actividad más desafiante de esta unidad para ti y por qué?
Definitivamente para mí la más desafiante fue la última activdad de apply en la que había que crear un ciclo para la sumatoria de números del 1 al 5. Inicialmente pensé que se haría fácil ya que en c# se puede hacer un for con i y hacer que se detenga cuando llegue a cierto valor pero me di cuenta que por tratarse de lenguaje ensamblador no había una forma sencilla de hacer un ciclo por lo que tuve que pensar ne la lógica y hacer que en una dirección se guardara el contador y en la otra la sumatoria.

##### La metodología de “predecir, ejecutar, observar y reflexionar” fue central en nuestras actividades. ¿En qué momento esta metodología te resultó más útil para entender algo que no tenías claro?
En general me gustó la metodología ya que a la hora de predecir podía ver lo que creía que sabía, al ejecutar podía olvidar los conocimientos erróneos previos y analizar por qué no funcionaron y cúal sería la forma correcta de hacerlo. Por último observar y reflexionar me permite ver qué conocimientos tengo interiorizados que serían los que realmente aprendí. En conclusión, usar esta metodología me servió para entender algo que antes no tenía claro, específicamente cuando confundía las etiquetas, antes pensaba que una etiqueta era @NOMBRE, después de analizar me di cuenta que tenía un error y en realidad las etiquetas son las que van entre paréntesis y mayúsculas, que pueden tener cualquier nombre y nos sirven para marcar partes del código.

##### Describe un momento “¡Aha!” que hayas tenido durante estas dos semanas. ¿Qué estabas haciendo cuando ocurrió?
Cuando leo un momento  “¡Aha!” pienso que se refiere a cuando funciona el código o entiendes algo en lo que estabas atascado. Para mí sería cuando entendí la diferencia de D = M y M = D, también cuando comprendí para qué servían y cómo usar etiquetas. Además cuando me di cuenta que se podía usar los saltos y no necesariamente se tenían que comparar siempre con 0 si no que podía poner antes en una línea por ejemplo D = D - A y luego al ser el salto se despejaría la operación y se compararía el valor de A.

##### Pensando en la próxima unidad, ¿Qué harás diferente en tu proceso de estudio para aprender de manera más efectiva?
Creo que nada, la verdad siento que seguí bien los pasos y fueron efectivos para mí, por lo que pienso seguir la misma metodología para la próxima unidad.

---

### Actividad 06
Coevaluación.

##### Encuentra un compañero de trabajo.
Estefania Aristizábal.

##### Intercambien las URLs de sus bitácoras de aprendizaje.
https://github.com/jfUPB/computacionales-2025-20-EstefaniaAO

##### Lee las entradas de tu compañero correspondientes a las actividades 01, 02, 03 y 04. Utilizando la rúbrica de la unidad, evalúa cada actividad y deja un comentario de retroalimentación por cada criterio. Recuerda ser específico y constructivo. Tu feedback debe ayudar a tu compañero a identificar sus fortalezas y áreas de oportunidad. Una vez que hayas terminado, comparte tus comentarios con tu compañero.

#### 1. Análisis del Ciclo Fetch-Decode-Execute y Programación Básica (Actividad 01)
Le doy un 5 porque cumple porque es completo y preciso y según la rúbrica cumple con lo siguiente: La bitácora contiene un reporte completo para ambos experimentos. Responde a todas las preguntas de análisis del primer programa de forma correcta. Presenta un programa funcional que suma 5 y 10 almacenando el resultado en la dirección 20. La explicación de la diferencia entre ROM y RAM es precisa. No hay omisiones.

###### Comentario: Buena organización y explicación muy profunda en cada una de las partes. Todos los códigos tienen comentarios en cada una de las líneas y además escribió qué no entendía y cómo sería la forma correcta de resolverlo. Toda la actividad está completa.

#### Identificación de Componentes y Estructuras de Control (Actividad 02)
Le doy un 5 porque cumple porque es completo y preciso y según la rúbrica cumple con lo siguiente: La bitácora responde de forma correcta y clara a las siete solicitudes: identifica una instrucción ALU válida y la explica, describe correctamente la función del PC, la diferencia entre los tipos de direccionamiento, los componentes para E/S, un bucle y una condición, explicando su funcionamiento en el contexto del programa.

###### Comentario: Hizo las predecciones de qué sucedería en cada una de las líneas, además señalo qué parte del código no entendía qué hacía y abajo la explicación. Demuestra que hizo un esfuerzo por entender el tema e investigar más allá. Toda la actividad está completa.

#### 3. Implementación de Control de Flujo con Saltos Condicionales (Actividad 03)
Le doy un 5 porque cumple porque es completo y preciso y según la rúbrica cumple con lo siguiente: La bitácora presenta un programa en ensamblador que es funcionalmente correcto y cumple con todos los requisitos del problema. Incluye un reporte del proceso de simulación paso a paso.

###### Comentario: Realizo predecciones en cada una de las parte del código que marcaba como correctas e incorrectas. Hay buena organización y responde a las preguntas requeridas. Toda la actividad está completa.

#### 4. Implementación de un Ciclo Simple para Acumulación (Actividad 04) Evalúa la respuesta a estas preguntas y solicitudes: Crear un programa que use un ciclo para sumar los números del 1 al 5 y guarde el resultado en la dirección de memoria 12. Reportar la simulación paso a paso.
Le doy un 5 porque cumple porque es completo y preciso y según la rúbrica cumple con lo siguiente: La bitácora presenta un programa en ensamblador que utiliza correctamente un ciclo para sumar los números del 1 al 5 y almacena el resultado final en la dirección de memoria 12. Incluye un reporte del proceso de simulación.

###### Comentario: Realizo predecciones en cada una de las parte del código que marcaba como correctas e incorrectas. Me gustó particularmente que al final hizo un resumen de lo que hacía el código. Toda la actividad está completa.
---

### Actividad 07
Feedback

##### Continuar: ¿Qué aspecto de las actividades, las explicaciones o la dinámica de la clase te ha resultado más útil o te ha gustado más y debería seguir haciendo?
Si todas las actividades, explicaciones y dínamicas de la clase me han gustado. Se aprende mucho tanto en clase como a la hora de resolver las actividades de la unidad.

##### Dejar de hacer: ¿Qué aspecto de la unidad te ha resultado confuso, poco útil o frustrante? ¿Hay algo que crees que debería eliminar o cambiar drásticamente?
Estoy satisfecha con la unidad pero a mi personalmente me costó pasar de entender código a programarlo. Yo podía ver un código y lo entendía pero si me pedían que lo escribiera desde 0 tenía problemas para empezar.

##### Empezar a hacer: ¿Qué te habría gustado que hiciéramos que no hicimos? ¿Tienes alguna idea para una actividad o un recurso que podría mejorar el aprendizaje en la próxima unidad?
No se me ocurre ninguno, me gustó cómo abordamos los temas con nano2tetris y github.

##### Ritmo y Dificultad: en una escala del 1 (muy fácil/lento) al 5 (muy difícil/rápido), ¿Cómo calificarías el ritmo y la dificultad general de esta unidad? ¿Por qué?
La verdad me pareció que la unidad hizo un salto muy drástico entre la primera actividad de apply y la segunda, le daría un 3 o 4 ya que para esa parte todavía estamos entendiendo y procesando esa nueva forma de programar. Las demás actividades me gustaron porque no las sentía muy fáciles ni muy difíciles si no como si a medida que avanzaramos se fuera incrementando la dificultad así que en general a la unidad le darái un 3.

##### Comentario Adicional: ¿Hay algo más que te gustaría compartir sobre tu experiencia de aprendizaje en esta unidad?
En general me gustó que desarrollaramos actividades de la unidad en clase ya que era posible hacer preguntas al respecto, los comentarios del profesor eran útiles y podía tomar nota en github para después analizarla con calma en mi propio tiempo.

