# Unidad 3


## 🤔 Fase: Reflect

### Actividad 11

#### Parte 1
1. Explica con tus propias palabras qué es el stack y qué es el heap en C++.

Ambos son parte de la memoria. El stack guarda variables locales y su memoria se libera automáticamente. El heap guarda objetos creados usando new y para borrar la memoria hay que especificarlo.

2. Describe las tres formas de pasar parámetros a una función en C++ (valor, referencia y puntero). Para cada una, explica qué sucede en memoria y cuándo usarías cada método.

Por valor crea una copia de la variable dentro de la función, por lo que cualquier cambio que se haga en esa copia y no afecta la original. Usaría este método cuando quiero trabajar con una copia y asegurar que el dato original no se modifique.

Por referencia se crea una especie de apodo para referirse al la variable original asi que lo que modifique en este apodo también se modifica en la original, porque los dos ocupan la misma dirección de memoria. La usaría para modificar el valor original.

Por puntero se toma la dirección del valor original y es posible modificar el valor. Lo usaría para cambiar el valor original a través de la dirección.

3. ¿Qué diferencia hay entre una variable local, una variable global y una variable local estática? ¿En qué segmento del mapa de memoria se almacena cada una?

Una variable local es la que está dentro de una función por lo que solo existe ahí, cuando se sale de la función la variabl deja de existir. Por otro lado está la variable global que es una que se puede usar en cualquier parte del código, incluso dentro de funciones donde no se ha definido esa variable. Finalmente, una variable local estática solo existe dentro de la función y además no se inicializa cada vez que se llama, solo la primera vez. Además cuando se vuelva a llamar la función esta toma el último valor asignado.

4. Explica qué es un objeto en C++ desde la perspectiva de memoria. ¿Dónde se almacenan los miembros de instancia y dónde los miembros estáticos?

Un objeto en C++ desde la perspectiva de la memoria es aquel que reserva un espacio en la memoria para guardar datos. Depende en qué tipo de memoria se guarden los miembros de instancia, si tiene new se guarda en el heap y si son variables locales se guardan en el stack. Los miembros estáticos como no son objetos pensaría que se guardan en otra parte.

#### Parte 2
~~~c++
**Predicción**
#include <iostream>
using namespace std;

class Enemigo {
public:
    static int totalEnemigos;
    int vida;
    int* armas;

    Enemigo(int v) : vida(v) {
        totalEnemigos++;
        armas = new int[3];
        armas[0] = 10; armas[1] = 15; armas[2] = 20;
    }
};

int Enemigo::totalEnemigos = 0;

void crearEscuadron() {
    for(int i = 0; i < 5; i++) {
        Enemigo soldado(100);
        soldado.vida -= 10;
    }
    cout << "Escuadrón creado. Total enemigos: " << Enemigo::totalEnemigos << endl;
}

int main() {
    crearEscuadron();
    crearEscuadron();
    return 0;
}
~~~

**Análisis**
identifica al menos dos problemas

**Solución**

#### Parte 3
**1. De todos los conceptos que exploraste en esta unidad (stack vs heap, paso de parámetros, ciclo de vida de objetos, etc.), ¿Cuál consideras que es el más crítico para evitar errores en programas reales? ¿Por qué?**

Considero que el más críticio para evitar errores es programación sería un buen manejo de memoria ya que al no tener esta práctica el programa se puede saturar el sistema y afectar el rendimiento. Por lo que hay que estar atentos a el ciclo de vida de los objetos en caso de que sea necesario destruirlos, también tener claro cómo funciona el heap o el stack es muy importante. También el paso de parámetros como valor, por referencia o puntero son muy utiles a la hora de programar y el uso adecuado permite crear un código eficiente.

**2.  ¿Cómo cambió tu comprensión sobre lo que realmente es un “objeto” después de comparar C++ con C#? ¿Qué implicaciones prácticas tiene esta diferencia?**
Cuando usaba c# para programar y creaba nuevos objetos lo hacía a través del new pero no sabía en dónde se guardaba o exactamente que hacía, simplemente lo asociaba con crear un nuevo objeto.

**4. Si tuvieras que explicar a un compañero de semestres anteriores por qué es importante entender la gestión de memoria en programación, ¿Qué le dirías en máximo 3 oraciones**
