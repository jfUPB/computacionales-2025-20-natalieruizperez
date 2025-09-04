# Evidencias para la unidad 4

## Código

Código para ofApp.h:

``` cpp
#pragma once
#include "ofMain.h"

// Nodo 
struct Node {
    float x, y;        // Posición 
    float radius;      // Tamaño del círculo
    ofColor color;     // Color
    float opacity;     // Opacidad
    Node* next;        // Puntero que va al siguiente nodo en la cola

    Node(float _x, float _y, float _radius, ofColor _color, float _opacity)
        : x(_x), y(_y), radius(_radius), color(_color), opacity(_opacity), next(nullptr) {
    }
};

// Implementación manual de una cola (FIFO)
class BrushQueue {
public:
    Node* front;    // Apunta al primer nodo creado de la cola (el más antiguo)
    Node* rear;     // apunta al último nodo de la cola (el más reciente)
    int size;      // Cantidad de nodos
    int maxSize;   // Cantidad máxima

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
    // Crea un nuevo nodo en el heap al final de la cola
    Node* newNode = new Node(x, y, radius, color, opacity);

	// Si la cola esta vacía el primer nodo creado es el primero y el último porque es el único elemento
    if (isEmpty()) {
        front = rear = newNode;
    }
	// Si ya tiene nodos, agrega otro al final (debajo del mouse)
	else {    
        rear->next = newNode;        
        rear = newNode;             // El nuevo nodo es el último en la cola
    }
    size++;
    
    // Si la cola supera `maxSize`, eliminar el nodo más antiguo con `dequeue()`
    if (size > maxSize) {
        dequeue();
    }
}

// Implementa aquí `dequeue()`
void BrushQueue::dequeue() {
    // Eliminar el nodo más antiguo si la cola no está vacía
    if (isEmpty()) return;
    
    Node* temp = front;       // Guarda la referencia del primer nodo (el primero en ser creado o el más antiguo)
    front = front->next;      // Apunta al siguiente
    delete temp; // Liberar memoria del nodo eliminado (el más antiguo)
    size--;      // Reduce el tamaño

	// Si esta vacía
    if (isEmpty()) {
        rear = nullptr;
    }
}

// Implementa aquí `clear()`
void BrushQueue::clear() {
    // Eliminar todos los nodos de la cola
    while (!isEmpty()) {
        dequeue();
    }
}

// Implementa aquí `isEmpty()`
bool BrushQueue::isEmpty() {
    // Retornar si la cola está vacía
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

    // Agregar un nuevo trazo si el mouse está presionado
    if (ofGetMousePressed()) {
        ofColor randomColor;
        randomColor.setHsb(ofRandom(255), 200, 255); // Color aleatorio
        float randomRadius = ofRandom(10, 30); // Radio entre 10-30
        strokes.enqueue(ofGetMouseX(), ofGetMouseY(), randomRadius, randomColor, 255.0f);  // Agregarlo a la cola
    }
}

//--------------------------------------------------------------
void ofApp::draw() {
    // Fondo con gradiente dinámico
    ofColor color1, color2;
    color1.setHsb(backgroundHue, 150, 240);
    color2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);
    ofBackgroundGradient(color1, color2, OF_GRADIENT_LINEAR);

    // Dibujar los trazos almacenados en la cola
    Node* current = strokes.front;
    int index = 0;
    
    // Recorre todos los nodos
    while (current != nullptr) {
        // Calcular opacidad
        float opacity = ofMap(index, 0, strokes.size - 1, 51, 255);
        ofSetColor(current->color, opacity);
        ofDrawCircle(current->x, current->y, current->radius);
        
        current = current->next;
        index++;
    }
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == 'c') {
        // Limpiar la cola de trazos
        strokes.clear();
    }
    if (key == 'a') {
        // Alternar entre 50 y 100 trazos
        strokes.maxSize = (strokes.maxSize == 50) ? 100 : 50;
        
        // Eliminar trazos excedentes si el nuevo tamaño es menor
        while (strokes.size > strokes.maxSize) {
            strokes.dequeue();
        }
    }
    else if (key == 's') {
        // Guardar el frame actual
        ofSaveScreen("captura_" + ofGetTimestampString() + ".png");
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

[Aquí está el video demostrativo de mi aplicación](https://youtu.be/UkvJMXIvmAo)


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
   










