# Unidad 3


## 🤔 Fase: Reflect

### Actividad 11

#### Parte 1
**1. Explica con tus propias palabras qué es el stack y qué es el heap en C++.**

Ambos son parte de la memoria. El stack guarda variables locales y su memoria se libera automáticamente. El heap guarda objetos creados usando new y para borrar la memoria hay que especificarlo.

**2. Describe las tres formas de pasar parámetros a una función en C++ (valor, referencia y puntero). Para cada una, explica qué sucede en memoria y cuándo usarías cada método.**

Por valor crea una copia de la variable dentro de la función, por lo que cualquier cambio que se haga en esa copia y no afecta la original. Usaría este método cuando quiero trabajar con una copia y asegurar que el dato original no se modifique.

Por referencia se crea una especie de apodo para referirse al la variable original asi que lo que modifique en este apodo también se modifica en la original, porque los dos ocupan la misma dirección de memoria. La usaría para modificar el valor original.

Por puntero se toma la dirección del valor original y es posible modificar el valor. Lo usaría para cambiar el valor original a través de la dirección.

**3. ¿Qué diferencia hay entre una variable local, una variable global y una variable local estática? ¿En qué segmento del mapa de memoria se almacena cada una?**

Una variable local es la que está dentro de una función por lo que solo existe ahí, cuando se sale de la función la variabl deja de existir. Por otro lado está la variable global que es una que se puede usar en cualquier parte del código, incluso dentro de funciones donde no se ha definido esa variable. Finalmente, una variable local estática solo existe dentro de la función y además no se inicializa cada vez que se llama, solo la primera vez. Además cuando se vuelva a llamar la función esta toma el último valor asignado.

**4. Explica qué es un objeto en C++ desde la perspectiva de memoria. ¿Dónde se almacenan los miembros de instancia y dónde los miembros estáticos?**

Un objeto en C++ desde la perspectiva de la memoria es aquel que reserva un espacio en la memoria para guardar datos. Depende en qué tipo de memoria se guarden los miembros de instancia, si tiene new se guarda en el heap y si son variables locales se guardan en el stack. Los miembros estáticos como no son objetos pensaría que se guardan en otra parte.

#### Parte 2

**Predicción**

``` c++
#include <iostream>
using namespace std;

class Enemigo {
public:
    static int totalEnemigos;          //Variable estatica que guarda el valor total de enemigos
    int vida;                          //La vida que ees un número entero
    int* armas;                        //Se crea un puntero

    Enemigo(int v) : vida(v) {        //Recibe una variable v y esa variable afecta la vida
        totalEnemigos++;              //Aumenta el número de enemigos cada vez que se ejecuta la clase
        armas = new int[3];           //Creo a través de int una dirección de memoria donde puedo guardar las armas en el heap
        armas[0] = 10; armas[1] = 15; armas[2] = 20;        //Aquí estoy asignandole a cada uno de los elementos de la lista un valor
    }
};

int Enemigo::totalEnemigos = 0;    //Le asigne a la clase enemigo un 0 en la variable total de enemigos

void crearEscuadron() {           //Una función que no devuelve nada
    for(int i = 0; i < 5; i++) {  //Un ciclo for que se repite hasta 5 veces
        Enemigo soldado(100);     //Creo un objeto de la clase Enemigo llamado soldado que tiene 100 de vida
        soldado.vida -= 10;       //Cada vez que se llama el ciclo le resto a esa vida 10
    }
    cout << "Escuadrón creado. Total enemigos: " << Enemigo::totalEnemigos << endl;   //Texto para mostrar el total de enemigos
}

int main() {
    crearEscuadron();          //Creo un escuadrón de 5
    crearEscuadron();          //Creo otro escuadrón pero esta vez de 10 porque se suman
    return 0;
}
```

**Análisis**
Lo primero que noto es que no hay un destructor para los elementos que se crean en el heap por lo que el programa podría saturarse por no liberar la memoria.

**Solución**

Aquí copie el código anterior y añadí el destructor.

``` c++
#include <iostream>
using namespace std;

class Enemigo {
public:
    static int totalEnemigos;          //Variable estatica que guarda el valor total de enemigos
    int vida;                          //La vida que ees un número entero
    int* armas;                        //Se crea un puntero

    Enemigo(int v) : vida(v) {        //Recibe una variable v y esa variable afecta la vida
        totalEnemigos++;              //Aumenta el número de enemigos cada vez que se ejecuta la clase
        armas = new int[3];           //Creo a través de int una dirección de memoria donde puedo guardar las armas en el heap
        armas[0] = 10; armas[1] = 15; armas[2] = 20;        //Aquí estoy asignandole a cada uno de los elementos de la lista un valor
    }
     ~Enemigo() {                      // Destructor para liberar la memoria
        delete[] armas;
    }
};

int Enemigo::totalEnemigos = 0;    //Le asigne a la clase enemigo un 0 en la variable total de enemigos

void crearEscuadron() {           //Una función que no devuelve nada
    for(int i = 0; i < 5; i++) {  //Un ciclo for que se repite hasta 5 veces
        Enemigo soldado(100);     //Creo un objeto de la clase Enemigo llamado soldado que tiene 100 de vida
        soldado.vida -= 10;       //Cada vez que se llama el ciclo le resto a esa vida 10
    }
    cout << "Escuadrón creado. Total enemigos: " << Enemigo::totalEnemigos << endl;   //Texto para mostrar el total de enemigos
}

int main() {
    crearEscuadron();          //Creo un escuadrón de 5
    crearEscuadron();          //Creo otro escuadrón pero esta vez de 10 porque se suman con el anterior
    return 0;
}
```

#### Parte 3
**1. De todos los conceptos que exploraste en esta unidad (stack vs heap, paso de parámetros, ciclo de vida de objetos, etc.), ¿Cuál consideras que es el más crítico para evitar errores en programas reales? ¿Por qué?**

Considero que el más críticio para evitar errores es programación sería un buen manejo de memoria ya que al no tener esta práctica el programa se puede saturar el sistema y afectar el rendimiento. Por lo que hay que estar atentos a el ciclo de vida de los objetos en caso de que sea necesario destruirlos, también tener claro cómo funciona el heap o el stack es muy importante. También el paso de parámetros como valor, por referencia o puntero son muy utiles a la hora de programar y el uso adecuado permite crear un código eficiente.

**2. ¿Cómo cambió tu comprensión sobre lo que realmente es un “objeto” después de comparar C++ con C#? ¿Qué implicaciones prácticas tiene esta diferencia?**

Cuando usaba c# para programar en unity, para crear nuevos objetos lo hacía a través del new pero no sabía en dónde se guardaba o exactamente que hacía, simplemente lo asociaba con crear un nuevo objeto. En esta unidad que trabajamos c++ entendí que es importante hacer una buena gestión de memoria y del ciclo de vida de los objetos. También recuerdo que en c# no era necesario un destructor por lo que me da la impresión de que c++ es más mecáico pero más preciso.

**3. Si tuvieras que explicar a un compañero de semestres anteriores por qué es importante entender la gestión de memoria en programación, ¿Qué le dirías en máximo 3 oraciones**

Entender la gestión de memoria es muy importante para que no hayan errores que hagan que el programa falle o sea lento. Si entiendes el stack y el heap podrás saber que sucede en la memoria de almacenamiento y así entender cuando es necesario destruir objetos para que el código sea funcional. Si no sabes de esto los programas que crees podrían ocupar mucha memoria.



