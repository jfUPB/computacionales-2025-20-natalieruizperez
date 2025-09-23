# Bitácora de aprendizaje de la unidad 6

Observar el comportamiento e interactuar con el código.

## Actividad 01
A cada una de las partículas del sistema le notificará qué tiene qué hacer. Las partículas observan un cambio de estado en la aplicación que es el subject y en la aplicación como tal va a ser el ofapp.
En el stup hay 3 ciclos para cerar tres tipos diferentes de partículas y es ahí donde se ingresala partícula que se está creando como ese cambio de estado que se va a observar.
La aplicación le pide al factory crear partícula creo en la memoria un tipo de partículo y luego se personaliza, se define el tamaño, color y en algunos casos la velocidad inciial. Lo único que se retorna a la aplicación es la dirección de memoria de la partícula.
Permite poner maquinas de estado

Cada que se destruye enl enemigo se le visa al intresado y se actualiza en la base de datos en la nube. Es un patrón que permite trabajar en equipo.

**1. ¿Cómo puedes interactuar con la aplicación? Menciona específicamente las teclas y qué efecto parecen tener sobre las partículas.**

**2.¿Observas los diferentes tipos de “partículas”? ¿Se comportan todas igual inicialmente?**

**Toma algunas capturas de pantalla de la aplicación en diferentes momentos (estado inicial, después de presionar ‘a’, ‘r’, ‘s’, ‘n’) y añádelas a tu bitácora.**

**¿Qué crees que está pasando “detrás de cámaras” cuando presionas las teclas? Formula una hipótesis inicial sobre cómo la aplicación cambia el comportamiento de las partículas.**

## Actividad 02

**1. Explica con tus propias palabras el propósito del patrón Observer. ¿Qué problema resuelve?**
**2. Dibuja un diagrama que muestre la relación entre Subject, Observer, ofApp y Particle en el caso de estudio, indicando quién es el Sujeto y quiénes los Observadores.**
**3. Construye un diagrama de secuencia que muestre cómo funciona el patrón Observer al presionar una tecla.**
**4. ¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.**
