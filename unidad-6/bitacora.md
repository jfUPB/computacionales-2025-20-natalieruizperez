# Bitácora de aprendizaje de la unidad 6

## Actividad 01

Observar el comportamiento e interactuar con el código.

**1. ¿Cómo puedes interactuar con la aplicación? Menciona específicamente las teclas y qué efecto parecen tener sobre las partículas.**

Puedo interactuar con la aplicación con las teclas s, a, r, y n como se puede ver en el código en esta parte:

``` c++
void ofApp::keyPressed(int key) {
  switch (key) {
  case 's':
    notify("stop");
    break;
  case 'a':
    notify("attract");
    break;
  case 'r':
    notify("repel");
    break;
  case 'n':
    notify("normal");
    break;
  default:
    break;
  }
}
```
El programa se ve como esferas que flotan por la pantalla lentamente en direcciones aleatorias:

<img width="1000" height="752" alt="image" src="https://github.com/user-attachments/assets/c4eeb30f-63d1-45b8-8ac1-889dbe915746" />

Al presionar la tecla "s" las esferas flotantes se detienen por completo en el punto en el que quedaron.

<img width="1000" height="744" alt="image" src="https://github.com/user-attachments/assets/7814a1eb-e7d5-421a-93b8-4ef577758d49" />

Cuando apreto la tecla "a" las esferas se reunen en el lugar en el que está el mouse, tiene sentido porque como dice en el código sucede "attract", este comportamiento me recordó a las esferas de agar.io. 

<img width="971" height="716" alt="image" src="https://github.com/user-attachments/assets/30926136-72f6-4d7c-94b7-829ec686d365" />

La tecla "r" hace todo lo contrario a la a, aquí las esferas huyen del mouse. 

<img width="999" height="745" alt="image" src="https://github.com/user-attachments/assets/3d797554-bff6-4c74-9f95-1038b07846f4" />

Finalmente la "n" se encarga de volver las esferas a una distribución similar a como estaban inicialmente, como una especie de reset pero este no funciona de forma inmediata si no que hace que las esferas vayan desde su posicioón a una más distribuida.

<img width="997" height="745" alt="image" src="https://github.com/user-attachments/assets/b135419a-81ef-4997-828a-922d2fc235cd" />


**2.¿Observas los diferentes tipos de “partículas”? ¿Se comportan todas igual inicialmente?**

Inicialmente las partículas se comportan de una forma muy similar ya que tienen una dirección aleaotira y rebotan con los bordes de la pantalla, pero lo que varía es que las verdes son las que tienen una velocidad menor, depués siguen las rojas hasta que finalmente las verdes son las más rápidas.

**3. Toma algunas capturas de pantalla de la aplicación en diferentes momentos (estado inicial, después de presionar ‘a’, ‘r’, ‘s’, ‘n’) y añádelas a tu bitácora.**

Las capturas las tomé en el punto anterior.

**¿Qué crees que está pasando “detrás de cámaras” cuando presionas las teclas? Formula una hipótesis inicial sobre cómo la aplicación cambia el comportamiento de las partículas.**

Al mirar el código por encima creo que al presionar las teclas en keypressed, este notifica el comportamiento a un estado para que se ejecute localizado en ofapp.h. Este estado creo que se encarga de actualizar la partícula cambiando los parámetros como la posción en x, y e inclusive la velocidad según la tecla que sea presionada.

---

## Actividad 02

**1. Explica con tus propias palabras el propósito del patrón Observer. ¿Qué problema resuelve?**

El propósito del patrón observer es notificar al objeto o no me quedó claro si era al usuario que ya sucedió una acción, creo que el problema que resuelve es que hace que los objetos no tengan que estar revisando constantemente si hubo algún cambio, si no que automáticamente notifica que sucedió. Es como si yo tuviese agregado en una app a carrito una camisa que me gustó y en lugar de revisar siempre si está disponible las apps de ropa acostumbran notificar al usuario cuando ya hay restock de ese producto para que lo puedan comprar.

**2. Dibuja un diagrama que muestre la relación entre Subject, Observer, ofApp y Particle en el caso de estudio, indicando quién es el Sujeto y quiénes los Observadores.**


**3. Construye un diagrama de secuencia que muestre cómo funciona el patrón Observer al presionar una tecla.**


**4. ¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.**

---

## Actividad 03

**1. Explica con tus propias palabras el propósito del patrón Factory Method (o Simple Factory, en este caso). ¿Qué problema principal aborda en la creación de objetos?**

**2. ¿Qué ventajas aporta el uso de ParticleFactory en ofApp::setup en comparación con instanciar y configurar las partículas directamente allí? Piensa en términos de organización del código (SRP - Single Responsibility Principle), legibilidad y facilidad para añadir nuevos tipos de partículas en el futuro.**

**3. Imagina que quieres añadir un nuevo tipo de partícula llamada "black_hole" que tiene tamaño grande, color negro y velocidad muy lenta. Describe los pasos que necesitarías seguir para implementar esto utilizando la ParticleFactory existente. ¿Tendrías que modificar ofApp::setup? ¿Por qué sí o por qué no?**

**4. El método createParticle en el ejemplo es estático. ¿Qué implicaciones (ventajas/desventajas) tiene esto comparado con tener una instancia de ParticleFactory y un método de instancia createParticle()?.**

---
## Actividad 04

**1. Explica con tus propias palabras el propósito del patrón State. ¿Cuándo es útil aplicarlo?**

**2. Dibuja un diagrama de estados simple para la clase Particle. Muestra los diferentes estados (Normal, Attract, Repel, Stop) como nodos y las transiciones entre ellos como flechas etiquetadas con el evento que las causa (p. ej., la tecla presionada: ‘n’, ‘a’, ‘r’, ‘s’).**

**3. Describe las ventajas de usar el patrón State en Particle en lugar de tener un miembro std::string estadoActual y usar un gran if/else if/else o switch dentro de Particle::update() para cambiar el comportamiento. Piensa en cohesión, extensibilidad (añadir nuevos estados) y el Principio Abierto/Cerrado (Open/Closed Principle).**

**4. ¿Qué responsabilidad tienen los métodos onEnter y onExit en el patrón State? Proporciona un ejemplo de por qué podrían ser útiles (incluso si no se usan mucho en todos los estados de este caso de estudio). Por ejemplo, ¿Qué podrías hacer en onEnter para AttractState o en onExit para StopState?**

---

## Actividad 05

En esta actividad modificarás el caso de estudio para añadir un nuevo tipo de partícula que utiliza los patrones Observer, Factory y State.

**ofApp.h:**
```

```

**ofApp.cpp:**
```

```

Explica cómo usaste el patrón Factory para esta nueva partícula.
Describe cómo implementaste el patrón Observer para esta nueva partícula.
Explica cómo aplicaste el patrón State a esta nueva partícula.

---
Notas de clase
A cada una de las partículas del sistema le notificará qué tiene qué hacer. Las partículas observan un cambio de estado en la aplicación que es el subject y en la aplicación como tal va a ser el ofapp.
En el stup hay 3 ciclos para cerar tres tipos diferentes de partículas y es ahí donde se ingresala partícula que se está creando como ese cambio de estado que se va a observar.
La aplicación le pide al factory crear partícula creo en la memoria un tipo de partículo y luego se personaliza, se define el tamaño, color y en algunos casos la velocidad inciial. Lo único que se retorna a la aplicación es la dirección de memoria de la partícula.
Permite poner maquinas de estado

Cada que se destruye enl enemigo se le avisa al intresado y se actualiza en la base de datos en la nube. Es un patrón que permite trabajar en equipo.

---
**Rúbrica**

Si usas IA para generar código, texto o imágenes la nota en esa actividad será 0.
Rúbrica de evaluación del proceso

5: realicé las 5 actividades completas y la autoevaluación.
4: realicé 4 actividades completas y la autoevaluación.
3: realicé 3 actividades completas y la autoevaluación.
2: realicé 2 actividades completas y la autoevaluación.
1: realicé 1 actividad completa y la autoevaluación.

---

## Nota 
-Actividad 01:
-Actividad 02:
-Activida 03:
-Actividad 04:
-Activida 05:
