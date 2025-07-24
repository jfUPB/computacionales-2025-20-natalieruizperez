# Unidad 1

## 🤔 Fase: Reflect

### Actividad 05
Sin consultar tus apuntes

---
#### Parte 01 : Recuperación de conocimiento (retrieval practice)

##### Describe con tus palabras las tres fases del ciclo Fetch-Decode-Execute. ¿Qué rol juega el Program Counter (PC) en este ciclo?

El Program Counter juega un papel importante en el ciclo ya que nos permite saber qué parte del programa se está ejecutando, además es posible ver los resultados línea por línea


##### ¿Cuál es la diferencia fundamental entre una instrucción-A (que empieza con @) y una instrucción-C (que involucra D, M, A, etc.) en el lenguaje ensamblador de Hack? Da un ejemplo de cada una.
La instrucción que empieza por @ es la que le asigna un valor a A, puede ser un número (@6, lo que quiere decir que A es 6) o una oración (@END, que le da el valor a A de END y sirve para ir a la etiqueta de esa instrucción si se pone un salto).

##### Explica la función de los siguientes componentes del computador Hack: el registro D, el registro A y la ALU.
El registro A es aquel que toma el valor que se le ponga a la hora de escribir @valor, en cambio el registro D no tiene forma de darle un valor dce forma directa, pero si es posible al relacionar a A con D diciendo que D = A. La ALU son las operaciones logarítmicas, creo recordar que significaba Algorithm Logic Unit que vendrían siendo operaciones como suma o resta por ejemplo D = D-A

##### ¿Cómo se implementa un salto condicional en Hack? Describe un ejemplo (p. ej., saltar si el valor de D es mayor que cero).
El salto condicional en el hack se implementa siempre y cuando se cumpla una condición. Por ejemplo si tengo @LOOP cuando D;JGT, es decir que haga un salto cuando D sea mayor o igual que 0, este irá al lugar en dónde puse la etiqueta.

##### ¿Cómo se implementa un loop en el computador Hack? Describe un ejemplo (p. ej., un loop que decremente un valor hasta que llegue a cero).

##### ¿Cuál es la diferencia entre la instrucción D=M y la instrucción M=D?
La diferencia entre la instrucción D=M y M=D es que en la primera instrucción se le está dando a D el valor que esté en la posición de la memoria de M, en cambio la segunda hace que la memoria tome el valor de D en la posición correspondiente mencionada.

##### Describe brevemente qué se necesita para leer un valor del teclado (KBD) y para “pintar” un pixel en la pantalla (SCREEN).
Para leer un valor del teclado se necesita la llamar a @KBD que equivale a 23476 y la etiqueta (KEYPRESSED) que toma un valor cuando una tecla es presionada. Por otro lado, para pintar un pixel en la pantalla es necesario llamar a @SCREEN que es 16384 y luego guardar el valor en la dirección 16.

--- 
#### Parte 2: Reflexión sobre tu proceso (metacognición)
##### ¿Cuál fue el concepto o actividad más desafiante de esta unidad para ti y por qué?
Definitivamente para mí la más desafiante fue la última activdad de apply en la que había que crear un ciclo para la sumatoria de números del 1 al 5. Inicialmente pensé que se haría fácil ya que en c# se puede hacer un for con i y hacer que se detenga cuando llegue a cierto valor pero me di cuenta que por tratarse de lenguaje ensamblador no había una forma sencilla de hacer un ciclo por lo que tuve que pensar ne la lógica y hacer que en una dirección se guardara el contador y en la otra la sumatoria.

##### La metodología de “predecir, ejecutar, observar y reflexionar” fue central en nuestras actividades. ¿En qué momento esta metodología te resultó más útil para entender algo que no tenías claro?
En general me gustó la metodología ya que a la hora de predecir podía ver lo que creía que sabía, al ejecutar podía olvidar los conocimientos erróneos previos y analizar por qué no funcionaron y cúal sería la forma correcta de hacerlo. Por último observar y reflexionar me permite ver qué conocimientos tengo interiorizados que serían los que realmente aprendí. En conclusión, usar esta metodología me servió para entender algo que antes no tenía claro, específicamente cuando confundía las etiquetas, antes pensaba que una etiqueta era @NOMBRE, después de analizar me di cuenta que tenía un error y en realidad las etiquetas son las que van entre paréntesis y mayúsculas, que pueden tener cualquier nombre y nos sirven para marcar partes del código.

##### Describe un momento “¡Aha!” que hayas tenido durante estas dos semanas. ¿Qué estabas haciendo cuando ocurrió?
Cuando leo un momento  “¡Aha!” pienso que se refiere a cuando funciona el código o entiendes algo en lo que estabas atascado. Para mí sería cuando entendí la diferencia de D = M y M = D, también cuando comprendí para qué servían y cómo usar etiquetas.

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
