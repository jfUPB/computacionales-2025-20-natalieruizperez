# Evidencias para la unidad 4

## Código

Código para ofApp.h:

``` cpp
#pragma once
#include "ofMain.h"

// Nodo de la cola
struct Node {
    float x, y;
    float radius;
    ofColor color;
    float opacity;
    Node* next;

    Node(float _x, float _y, float _radius, ofColor _color, float _opacity)
        : x(_x), y(_y), radius(_radius), color(_color), opacity(_opacity), next(nullptr) {
    }
};

// Implementación cola
class BrushQueue {
public:
    Node* front;
    Node* rear;
    int size;
    int maxSize;

    BrushQueue(int _maxSize);
    ~BrushQueue();

    void enqueue(float x, float y, float radius, ofColor color, float opacity);
    void dequeue();
    void clear();
    bool isEmpty();
};


// Constructor
BrushQueue::BrushQueue(int _maxSize) : front(nullptr), rear(nullptr), size(0), maxSize(_maxSize) {}

// Destructor
BrushQueue::~BrushQueue() {
    clear();
}

// Implementa aquí `enqueue()`
void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity) {
    // TODO: crear un nuevo nodo y agregarlo al final de la cola.
    // Si la cola supera `maxSize`, eliminar el nodo más antiguo con `dequeue()`.
    Node* newNode = new Node(x, y, radius, color, opacity);
    
    if (isEmpty()) {
        front = rear = newNode;
    } else {
        rear->next = newNode;
        rear = newNode;
    }
    size++;
    
    if (size > maxSize) {
        dequeue(); // Elimina el nodo más antiguo si se excede el tamaño
    }
}

// Implementa aquí `dequeue()`
void BrushQueue::dequeue() {
    // TODO: eliminar el nodo más antiguo si la cola no está vacía.
    if (isEmpty()) return;
    
    Node* temp = front;
    front = front->next;
    delete temp; // Se libera la memoria del nodo
    size--;
    
    if (isEmpty()) {
        rear = nullptr;
    }
}

// Implementa aquí `clear()`
void BrushQueue::clear() {
    // TODO: eliminar todos los nodos de la cola.
    while (!isEmpty()) {
        dequeue(); // Se libera memoria de todos los nodos
    }
}

// Implementa aquí `isEmpty()`
bool BrushQueue::isEmpty() {
    // TODO: retornar si la cola está vacía.
    return front == nullptr;
}


class ofApp : public ofBaseApp {
public:
    BrushQueue strokes; // Cola de trazos
    float backgroundHue = 0;

    ofApp() : strokes(50) {} // Tamaño máximo de la cola

    void setup();
    void update();
    void draw();
    void keyPressed(int key);
};

```

Código para ofApp.cpp:

``` cpp
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {
    ofBackground(0);
}

//--------------------------------------------------------------
void ofApp::update() {
    backgroundHue += 0.2;
    if (backgroundHue > 255) backgroundHue = 0;

    // TODO: agregar un nuevo trazo si el mouse está presionado.
    // Usa strokes.enqueue(x, y, radius, color, opacity);
    if (ofGetMousePressed()) {
        ofColor randomColor = ofColor::fromHsb(ofRandom(255), 200, 255);
        float randomRadius = ofRandom(10, 30);
        strokes.enqueue(ofGetMouseX(), ofGetMouseY(), randomRadius, randomColor, 1.0f);
    }
}

//--------------------------------------------------------------
void ofApp::draw() {
    // Fondo con gradiente dinámico
    ofColor color1, color2;
    color1.setHsb(backgroundHue, 150, 240);
    color2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);
    ofBackgroundGradient(color1, color2, OF_GRADIENT_LINEAR);

    // TODO: dibujar los trazos almacenados en la cola.
    // Recorre los nodos desde strokes.front hasta nullptr y usa ofDrawCircle().
    Node* current = strokes.front;
    int position = 0;
    
    while (current != nullptr) {
        // Calcular opacidad basada en la posición en la cola (20% a 100%)
        float minOpacity = 0.2f;
        float maxOpacity = 1.0f;
        float calculatedOpacity;
        
        if (strokes.size == 1) {
            calculatedOpacity = maxOpacity;
        } else {
            float t = static_cast<float>(position) / (strokes.size - 1);
            calculatedOpacity = minOpacity + t * (maxOpacity - minOpacity);
        }
        
        ofSetColor(current->color, calculatedOpacity * 255);
        ofDrawCircle(current->x, current->y, current->radius);
        
        current = current->next;
        position++;
    }
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == 'c') {
        // TODO: limpiar la cola de trazos.
        strokes.clear(); // Se libera la memoria
    }
    if (key == 'a') {
        // TODO: alternar entre 50 y 100 trazos.
        if (strokes.maxSize == 50) {
            strokes.maxSize = 100;
        } else {
            strokes.maxSize = 50;
        }
        
        // Eliminar trazos excedentes si el nuevo tamaño máximo es menor
        while (strokes.size > strokes.maxSize) {
            strokes.dequeue(); // Se libera memoria de nodos
        }
    }
    else if (key == 's') {
        // TODO: guardar el frame actual.
        ofSaveFrame();
    }
}

```

Código para main.cpp:
``` cpp
#include "ofMain.h"
#include "ofApp.h"

//========================================================================
int main( ){

	//Use ofGLFWWindowSettings for more options like multi-monitor fullscreen
	ofGLWindowSettings settings;
	settings.setSize(1024, 768);
	settings.windowMode = OF_WINDOW; //can also be OF_FULLSCREEN

	auto window = ofCreateWindow(settings);

	ofRunApp(window, std::make_shared<ofApp>());
	ofRunMainLoop();

}
```

## Demostración:

[Aquí está el video demostrativo de mi aplicación](https://youtu.be/ieQNZ1EfYkk)


---
### Toma de nota para mí

-En la clase ofApp qe hereda a ofBaseApp se va a crear un paquete de datos que va a tener la aplicacion, ahí no se definen variables. Setup se llama una vez es donde se hacen las configuraciones iniciales. Update se actualizan variables y en draw solamente dibujo con las variables que actualice en update, ambas funciones se actualizan cada segundo.  Los eventos son declarados en esta clase.

-En el ofApp.cpp es donde están las definicinioes pero ahí no han sido declaradas.

-Voy al ofApp.h que tiene lo que necesita mi aplicación.

El objeto va a tener todos los atributos que vienen de cp m{as los nuevos de .h, el objeto cpp se va a crear en el heap.

**Diferencia entre cpp y .h**

  .h declaramos cpp definimos

  Head es el untero de la lista, si está en null no tengo que hacer nada y push manda a la lista al final.

Voy a mapear el index y este puede tomar valores entre cero y el tamaño de la cola menos uno. Una vez creo ls nodos y defino los vertices le digo a la cpu que dibuje la línea.


Hay que implementar a mano una fifo para el apply, no una lista de datos. Yo creo un elemento y el siguiente elemento está al lado, los elementos se pueden conectar pero al procesarlos lo hacen en el orden qe se crearon. Tiene que star implementado de forma maual , no se pueden usar librerías.
   








