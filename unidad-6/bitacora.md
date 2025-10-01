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

<img width="1035" height="745" alt="image" src="https://github.com/user-attachments/assets/1f786d7a-babd-4701-87c7-dad81751f71b" />

Los sujetos serían Subject (que es la clase padre) y ofApp (que la hereda), estas se encargan de notificar a los observadores que son Observer (clase padre) y Particle( que la hereda).


**3. Construye un diagrama de secuencia que muestre cómo funciona el patrón Observer al presionar una tecla.**

AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA


**4. ¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.**

Creo que al tener el sistema del observer es mejor ya que no se está actualizando en cada frame como en el update, si no que unicamente cambian su comportamiento cuando reciben la notificación. Las partículas no están directamente relacionadas entre si por lo que tienen menor acomplamiento y como los objetos dependen de la notificación hay más extensibilidiad y facilidad para agregar nuevos objetos y otras cosas.

---

## Actividad 03

**1. Explica con tus propias palabras el propósito del patrón Factory Method (o Simple Factory, en este caso). ¿Qué problema principal aborda en la creación de objetos?**

El Factory Method tiene como propósito simplificar procesos y que sea más flexible porque no hay que escribirlo cada vez que quiero crear un objeto. Ejemplo en el código donde se usa:

**Código:**
```
Particle * ParticleFactory::createParticle(const std::string & type) {
  Particle * particle = new Particle();

  if (type == "star") {
    particle->size = ofRandom(2.0f, 4.0f);
    particle->color = ofColor(255, 0, 0);
  } else if (type == "shooting_star") {
    particle->size = ofRandom(3.0f, 6.0f);
    particle->color = ofColor(0, 255, 0);
    particle->velocity *= 3.0f;
  } else if (type == "planet") {
    particle->size = ofRandom(5.0f, 8.0f);
    particle->color = ofColor(0, 0, 255);
  }
  return particle;
}
```
El problema principal que aborda la creación de objetos es el tener que instanciar manualmente cada objeto y cambiarle parámetros. A través del Factory Method es más sencillo porque solo pongo que tipo es crea el objeto con los valores que corresponden. Además en caso de querer agregar otro objeto diferente no tendría que modificar el código anterior, simplemente agregar un nuevo tipo.

**2. ¿Qué ventajas aporta el uso de ParticleFactory en ofApp::setup en comparación con instanciar y configurar las partículas directamente allí? Piensa en términos de organización del código (SRP - Single Responsibility Principle), legibilidad y facilidad para añadir nuevos tipos de partículas en el futuro.**

El ParticleFactory permite tiene una ventaja grande ya que en lugar de instanciar y configurar las partúculas manualmente me ahorro ese paso y puedo por así decirlo categorizar cada uno de los tipos que quiero. Es un código mucho más legible, limpio y además funcional ya que no tiene grandes niveles de dependencia y en caso de yo querer agregar una partícula lo hago simplemente poniendo otro tipo.

**3. Imagina que quieres añadir un nuevo tipo de partícula llamada "black_hole" que tiene tamaño grande, color negro y velocidad muy lenta. Describe los pasos que necesitarías seguir para implementar esto utilizando la ParticleFactory existente. ¿Tendrías que modificar ofApp::setup? ¿Por qué sí o por qué no?**

En caso de crear esa nueva partícula si necesito modificar el ofApp::setup porque ahí es donde se agregan como observadores y también defino el tipo y la cantidad, pero se puede hacer de forma sencilla. Lo qe debería de hacer para implementarlo en la ParticleFactory sería primero agregar en el ofApp "black_hole" y luego en el ParticleFactory definir los parámetros.

**ofApp**
```
  for (int i = 0; i < 3; ++i) {
    Particle * p = ParticleFactory::createParticle("black_hole");
    particles.push_back(p);
    addObserver(p);
  }
```

**ParticleFactory**
```
else if (type == "black_hole") {
    particle->size = ofRandom(100.0f, 150.0f);
    particle->color = ofColor(0, 0, 0);
    particle->velocity *= 0.1f;
```

**4. El método createParticle en el ejemplo es estático. ¿Qué implicaciones (ventajas/desventajas) tiene esto comparado con tener una instancia de ParticleFactory y un método de instancia createParticle()?.**

El método createParticle tiene sentido que sea estático porque no tengo que crear un objeto para usarlom además es ventajoso porque así no confundirme añadiendo cosas que no debería pero si necesitara guardar algo o hacer cosas con la fábrica, entonces no sería estático. Ambas tienen sus ventajas y desventajas entonces depende de lo que quiera hacer.

---
## Actividad 04

**1. Explica con tus propias palabras el propósito del patrón State. ¿Cuándo es útil aplicarlo?**

El patron State sirve para hacer que ocurran eventos egún las acciones que se realizan. Un ejemplo sería cuando en el celular se apreta una tecla de número el sistema recibe es ocomo acción y el evento sería mostrar ese número en la pantalla. Es útil aplicalrlo cuando quiero que obtener un resultado determinado al realizar una acción.

El patrón State sirve para cambiar el comportamiento de un objeto según las acciones que se realizan y el estado en el que este. Es como hacer que ocurran diferentes acciones según la situación actual. Por ejemplo, en un celular, si presiono una tecla, el sistema detecta esa acción y, dependiendo del estado (como si está bloqueado o no), puede mostrar el número o no hacer nada.
Este patrón es útil cuando quiero que un objeto tenga distintos comportamientos sin tener que usar muchos if o switch, y cuando esos comportamientos cambian dependiendo del estado en el que esté.

**2. Dibuja un diagrama de estados simple para la clase Particle. Muestra los diferentes estados (Normal, Attract, Repel, Stop) como nodos y las transiciones entre ellos como flechas etiquetadas con el evento que las causa (p. ej., la tecla presionada: ‘n’, ‘a’, ‘r’, ‘s’).**

AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA

**3. Describe las ventajas de usar el patrón State en Particle en lugar de tener un miembro std::string estadoActual y usar un gran if/else if/else o switch dentro de Particle::update() para cambiar el comportamiento. Piensa en cohesión, extensibilidad (añadir nuevos estados) y el Principio Abierto/Cerrado (Open/Closed Principle).**

La ventaja que tiene al tener un patron State en Particle en lugar de un estadoActual es que además de que uno se ahorra líneas de código sirve para que el código sea más compacto y a la hora de añadir un nuevo estado no tengo que crear otros condicionales si no simplemente creo una nueva clase. Tuve que buscar que era el principio de abierto cerrado porque no recordaba y si lo cumple porque es fácil agregar cosas sin necesidad de modificar lo ya existente.

**4. ¿Qué responsabilidad tienen los métodos onEnter y onExit en el patrón State? Proporciona un ejemplo de por qué podrían ser útiles (incluso si no se usan mucho en todos los estados de este caso de estudio). Por ejemplo, ¿Qué podrías hacer en onEnter para AttractState o en onExit para StopState?**

Esos métodos son responsables de hacer cosas cuando se entra o se sale de un estado. Por ejemplo, en onEnter de AttractState podría cambiar el color de la partícula cuando este siendo atraída y en onExit de StopState volverle a poner el color original cuando salga del estado. 

---

## Actividad 05

En esta actividad modificarás el caso de estudio para añadir un nuevo tipo de partícula que utiliza los patrones Observer, Factory y State. 

Decidí añadir la misma partícula del ejemplo pasado de black_hole porque ya había hecho una parte del código solo que puse le fondo en blanco para que se pudieran ver las nuevas partícula nuevas ya que son negras.

**ofApp.h:**
```
#pragma once

#include "ofMain.h"
#include <string>
#include <vector>

class Observer {
public:
	virtual ~Observer() = default;
	virtual void onNotify(const std::string & event) = 0;
};

class Subject {
public:
	void addObserver(Observer * observer);
	void removeObserver(Observer * observer);

protected:
	void notify(const std::string & event);

private:
	std::vector<Observer *> observers;
};

class Particle;

class State {
public:
	virtual ~State() = default;
	virtual void update(Particle * particle) = 0;
	virtual void onEnter(Particle * particle) { }
	virtual void onExit(Particle * particle) { }
};

class Particle : public Observer {
public:
	Particle();
	~Particle() override;

	Particle(const Particle &) = delete;
	Particle & operator=(const Particle &) = delete;

	void update();
	void draw();
	void onNotify(const std::string & event) override;

	void setState(State * newState);

	ofVec2f position;
	ofVec2f velocity;
	float size;
	ofColor color;

private:
	void keepInsideWindow();
	State * state;
};

class NormalState : public State {
public:
	void update(Particle * particle) override;
	void onEnter(Particle * particle) override;
};

class AttractState : public State {
public:
	void update(Particle * particle) override;
};

class RepelState : public State {
public:
	void update(Particle * particle) override;
};

class StopState : public State {
public:
	void update(Particle * particle) override;
};

class ParticleFactory {
public:
	static Particle * createParticle(const std::string & type);
};

class ofApp : public ofBaseApp, public Subject {
public:
	~ofApp() override;
	void setup() override;
	void update() override;
	void draw() override;
	void keyPressed(int key) override;

private:
	std::vector<Particle *> particles;
};

```

**ofApp.cpp:**
```
#include "ofApp.h"
#include <algorithm>

void Subject::addObserver(Observer * observer) {
	if (!observer) return;
	if (std::find(observers.begin(), observers.end(), observer) == observers.end()) {
		observers.push_back(observer);
	}
}

void Subject::removeObserver(Observer * observer) {
	if (!observer) return;
	observers.erase(std::remove(observers.begin(), observers.end(), observer), observers.end());
}

void Subject::notify(const std::string & event) {
	for (Observer * observer : observers) {
		observer->onNotify(event);
	}
}

Particle::Particle()
	: state(nullptr) {
	position = ofVec2f(ofRandomWidth(), ofRandomHeight());
	velocity = ofVec2f(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
	size = ofRandom(2.0f, 5.0f);
	color = ofColor(255);

	state = new NormalState();
	state->onEnter(this);
}

Particle::~Particle() {
	if (state) {
		state->onExit(this);
		delete state;
		state = nullptr;
	}
}

void Particle::setState(State * newState) {
	if (state) {
		state->onExit(this);
		delete state;
	}
	state = newState;
	if (state) {
		state->onEnter(this);
	}
}

void Particle::update() {
	if (state) {
		state->update(this);
	}
	keepInsideWindow();
}

void Particle::draw() {
	ofPushStyle();
	ofSetColor(color);
	ofDrawCircle(position, size);
	ofPopStyle();
}

void Particle::onNotify(const std::string & event) {
	if (event == "attract") {
		setState(new AttractState());
	} else if (event == "repel") {
		setState(new RepelState());
	} else if (event == "stop") {
		setState(new StopState());
	} else if (event == "normal") {
		setState(new NormalState());
	}
}

void Particle::keepInsideWindow() {
	const float W = static_cast<float>(ofGetWidth());
	const float H = static_cast<float>(ofGetHeight());

	if (position.x < 0.0f) {
		position.x = 0.0f;
		velocity.x *= -1.0f;
	} else if (position.x > W) {
		position.x = W;
		velocity.x *= -1.0f;
	}
	if (position.y < 0.0f) {
		position.y = 0.0f;
		velocity.y *= -1.0f;
	} else if (position.y > H) {
		position.y = H;
		velocity.y *= -1.0f;
	}
}

void NormalState::onEnter(Particle * particle) {
	particle->velocity.set(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
}

void NormalState::update(Particle * particle) {
	particle->position += particle->velocity;
}

static void steer(Particle * particle, const ofVec2f & toward, float accel, float vmax, float posScale) {
	ofVec2f dir = toward - particle->position;
	float len = dir.length();
	if (len > 1e-6f) {
		dir /= len;
		particle->velocity += dir * accel;
	}
	particle->velocity.limit(vmax);
	particle->position += particle->velocity * posScale;
}

void AttractState::update(Particle * particle) {
	ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
	steer(particle, mouse, /*accel*/ 0.05f, /*vmax*/ 3.0f, /*posScale*/ 0.2f);
}

void RepelState::update(Particle * particle) {
	ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
	ofVec2f away = particle->position - mouse;
	float len = away.length();
	if (len > 1e-6f) {
		away /= len;
		particle->velocity += away * 0.05f;
	}
	particle->velocity.limit(3.0f);
	particle->position += particle->velocity * 0.2f;
}

void StopState::update(Particle * particle) {
	particle->velocity *= 0.80f;
	if (particle->velocity.lengthSquared() < 1e-4f) {
		particle->velocity.set(0.0f, 0.0f);
	}
	particle->position += particle->velocity;
}

Particle * ParticleFactory::createParticle(const std::string & type) {
	Particle * particle = new Particle();

	if (type == "star") {
		particle->size = ofRandom(2.0f, 4.0f);
		particle->color = ofColor(255, 0, 0);
	} else if (type == "shooting_star") {
		particle->size = ofRandom(3.0f, 6.0f);
		particle->color = ofColor(0, 255, 0);
		particle->velocity *= 3.0f;
	} else if (type == "planet") {
		particle->size = ofRandom(5.0f, 8.0f);
		particle->color = ofColor(0, 0, 255);
	} else if (type == "black_hole") {
		particle->size = ofRandom(100.0f, 150.0f);
		particle->color = ofColor(0, 0, 0);
		particle->velocity *= 0.1f;
	}
	return particle;
}

ofApp::~ofApp() {
	for (Particle * p : particles) {
		removeObserver(p);
		delete p;
	}
	particles.clear();
}

void ofApp::setup() {
	ofBackground(255);
	particles.reserve(100 + 5 + 10);

	for (int i = 0; i < 100; ++i) {
		Particle * p = ParticleFactory::createParticle("star");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 5; ++i) {
		Particle * p = ParticleFactory::createParticle("shooting_star");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 10; ++i) {
		Particle * p = ParticleFactory::createParticle("planet");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 3; ++i) {
		Particle * p = ParticleFactory::createParticle("black_hole");
		particles.push_back(p);
		addObserver(p);
	}

}

void ofApp::update() {
	for (Particle * p : particles) {
		p->update();
	}
}

void ofApp::draw() {
	for (Particle * p : particles) {
		p->draw();
	}
}

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
Al abrir el programa

<img width="1012" height="682" alt="image" src="https://github.com/user-attachments/assets/c80838fd-01e6-4cef-b6da-4461f0b057ce" />

Al presionar "a"

<img width="1013" height="672" alt="image" src="https://github.com/user-attachments/assets/2cb906d9-4e63-47bd-bc41-195296a5e1bd" />

Al presionar "n"

<img width="1006" height="681" alt="image" src="https://github.com/user-attachments/assets/79ddfb19-6e95-4e99-82f1-8db68ec67bf0" />

Al presionar "s"

<img width="961" height="646" alt="image" src="https://github.com/user-attachments/assets/87b97a8e-d004-40b1-b35f-b687b3d0f2b3" />

Y al presionar "r"
<img width="1009" height="686" alt="image" src="https://github.com/user-attachments/assets/830abf80-2bab-4d4c-a5cb-c3fde4418f41" />


**Explica cómo usaste el patrón Factory para esta nueva partícula.**

Cree la partícula "black_hole" en ParticleFactory::createParticle y modifique los parámetros para que quedara con las características que yo quisiera.

**Describe cómo implementaste el patrón Observer para esta nueva partícula.**

El patron observer ya estaba en el código y como esta seteado para todas las partículas esta nueva que puse se volvió observer. Esto quiere decir que están esperando al ser notificadas cuando se presionen las teclas por lo que funcionan igual que las otras partículas.

**Explica cómo aplicaste el patrón State a esta nueva partícula.**

Los estados ya los tenía porque los hereda entonces reacciona a cada uno de ellos según en el que este.

**Conclusión**

Crear una nueva partícula fue muy fácil porque el código estaba bien diseñado en los patrones Observer, Factory y State. No tuve que modificar muchas cosas, solo agregar el nuevo tipo de partícula y  ahi mismo heredó los estados y empezó a reaccionar a los eventos. Es por esto que es importante tener buenos patrones de diseño, poca dependencia y un orden en el código.

---

**Notas de clase**

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

## Nota: 5.0
-Actividad 01: Completa (5.0)
-Actividad 02: Completa (5.0)
-Activida 03: Completa  (5.0)
-Actividad 04: Completa (5.0)
-Activida 05: Completa  (5.0)
