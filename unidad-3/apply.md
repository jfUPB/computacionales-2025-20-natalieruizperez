# Unidad 3


## 🛠 Fase: Apply

### Actividad 06

**Programa c++**

<img width="1097" height="563" alt="image" src="https://github.com/user-attachments/assets/4b57c7d8-0aad-4755-9da0-9fd3a2ab4373" />

**Contenido de la memoria**

<img width="340" height="60" alt="image" src="https://github.com/user-attachments/assets/354ed0ad-c295-478f-9b16-9f4b045e6371" />

**Calculadora**

Al escribir 0a en la calculadora, cambiar a modo de programador y ponerlo en hexadecimal obtengo como valor el número 10.

<img width="311" height="521" alt="image" src="https://github.com/user-attachments/assets/bf6f8041-08e8-440b-be06-6d417b3f32d4" />

Al escribir 14 en hex obtengo como valor 20.

<img width="314" height="525" alt="image" src="https://github.com/user-attachments/assets/bc115854-64bd-4344-84ce-7d66563206be" />

Si la arquitectura de tu computador fuera big-endian, ¿Cómo quedarían almacenados los bytes en la memoria de p?

#### Reflexión
**1. ¿Cuál es la diferencia entre un constructor y un destructor en C++?**

  La diferencia entre el constructor y el destructor en c++ es en cuanto a la escritura, ya que un constructor es el nombre del objeto creado y para el destructor escribo lo mismo pero con este simbolo "~". Además el destructor no recibe parámetros.

**2. ¿Cuál es la diferencia entre un objeto y una clase en C++?**
Un objeto en c++ se puede crear o destruir, mientras que es posible acceder a una clase o salir de esta pero nunca destruirla. Además es posible crear varios objetos.

**3. ¿Qué diferencia notas entre el objeto Punto en C++ y C#?**
En c# solo se puede crear en el heap, mientras que en c++ se crea en el stack y en el heap.

**4. ¿Qué es p en C++ y qué es p en C#? (en uno de ellos p es un objeto y en el otro es una referencia a un objeto).**
En c++ es un objeto ya que es creado en el stack, mientras que en c# p es una referencia al objeto en heap.

**5. ¿En qué parte de memoria se almacena p en C++ y en C#?**
En c++ el objeto en el stack se almacena en una posición de la memoria 0a 00 00 00 14 00 00 00, mientras que en c# se accede a esa referencia en el heap.

**6. ¿Qué observaste con el depurador acerca de p? Según lo que observaste ¿Qué es un objeto en C++?**
Según mis observaciones un objeto en c++ ocupa una dirección en la memoria donde es almacenada. Adicionalmente es posible crear y destruirlos y puedo crear cuantos quiera siempre y cuanto me lo permita la memoria.

---
### Actividad 07

**Ejecución del programa**

#### Reflexión
**1. Explicación de la diferencia entre objetos creados en el stack y en el heap.**



**2. pStack ¿Es un objeto o una referencia a un objeto?**

**3. pHeap ¿Es un objeto o una referencia a un objeto? Si es una referencia, ¿A qué objeto hace referencia?**

**4. Observa en Memory1 (Debug->Windows->Memory->Memory1) el contenido de la dirección de memoria de pHeap, recuerda escribir en la entrada de texto de Memory1 la dirección de memoria de &pHeap y presionar Enter. Compara el contenido de memoria con el contenido de pHeap en la pestaña de Locals (Debug->Windows->Locals). ¿Qué observas? ¿Qué significa esto?**

---
### Actividad 08


### Actividad integradora de aplicación

#### Parte 1
**1. Explica con tus propias palabras qué es el stack y qué es el heap en C++.**


**2. Describe las tres formas de pasar parámetros a una función en C++ (valor, referencia y puntero). Para cada una, explica qué sucede en memoria y cuándo usarías cada método.**

**3. ¿Qué diferencia hay entre una variable local, una variable global y una variable local estática? ¿En qué segmento del mapa de memoria se almacena cada una?**

Una variable local es la que está dentro de una función por lo que solo existe ahí, cuando se sale de la función la variabl deja de existir. Por otro lado está la variable global que es una que se puede usar en cualquier parte del código, incluso dentro de funciones donde no se ha definido esa variable. Finalmente, una variable local estática solo existe dentro de la función y además no se inicializa cada vez que se llama, solo la primera vez. Además cuando se vuelva a llamar la función esta toma el último valor asignado.

**4. Explica qué es un objeto en C++ desde la perspectiva de memoria. ¿Dónde se almacenan los miembros de instancia y dónde los miembros estáticos?**

#### Parte 2
**1. Diagnóstico del problema**

<img width="831" height="250" alt="image" src="https://github.com/user-attachments/assets/6e0ad279-9a9f-4ec7-be53-7a872b97e486" />

  Primero voy a observar qué está pasando en la clase personaje. Veo que se están creando variables y que hay una especie de puntero para manejar las estádisticas. Además veo que no hay un destructor, esto sería un error ya que se apunta a una posición de la memoria y en heap se crea un nuevo elemento pero nunca se elimina. Como consecuencia, estaría ocupando memoria innecesaria que podría aprovecharse para algo más. Otro error sería que se salta la función imprimir, como consecuencia es como si no estuviese.

<img width="952" height="394" alt="image" src="https://github.com/user-attachments/assets/bb5c0216-fe90-4e0e-86ae-513714018848" />


  Ahora voy a observar que está pasando en la función simularEncuentro. Veo que hay un texto que indica que se está iniciando el encuentro y también que se crea un objeto personaje al que se llama heroe y después se crea una variable que es "la copia" de heroe. Después se accede al parámetro del nombre y se le cambia para que no tenga el mismo nombre que el heroe. Aquí el error que veo es que al analizar a fondo ambas estadísticas se están guardando en la misma dirección de memoria. Como consecuencia, cuando modifique una estadística del heroe se modificará también el de la de la copia.

<img width="356" height="64" alt="image" src="https://github.com/user-attachments/assets/4e74dd98-8c07-4c02-a652-852bb2b6551b" />
  
<img width="338" height="59" alt="image" src="https://github.com/user-attachments/assets/e5ffa565-92e2-4e9f-a1c9-9d7beb5a4f53" />


**2. Solución**

 ```c++
#include <iostream>
#include <string>

class Personaje {
public:
    std::string nombre;
    int* estadisticas;

    Personaje(std::string n, int vida, int ataque, int defensa) {
        nombre = n;
        estadisticas = new int[3];
        estadisticas[0] = vida;
        estadisticas[1] = ataque;
        estadisticas[2] = defensa;
        std::cout << "Constructor: nace " << nombre << std::endl;
    }

    ~Personaje() {
        delete[] estadisticas;
        std::cout << "Destructor: muere " << nombre << std::endl;
    }


    void imprimir() {
        std::cout << "Personaje " << nombre
            << " [Vida: " << estadisticas[0]
            << ", ATK: " << estadisticas[1]
            << ", DEF: " << estadisticas[2]
            << "]" << std::endl;
    }
};

void simularEncuentro() {
    std::cout << "\n--- Iniciando encuentro ---" << std::endl;
    Personaje heroe("Aragorn", 100, 20, 15);

    heroe.imprimir();

    Personaje copiaHeroe("Copia de Aragorn",
        heroe.estadisticas[0],
        heroe.estadisticas[1],
        heroe.estadisticas[2]);

    copiaHeroe.estadisticas[0] = 40;

    copiaHeroe.imprimir();

    std::cout << "Saliendo del encuentro..." << std::endl;
}

int main() {
    simularEncuentro();
    std::cout << "\nSimulación terminada." << std::endl;
    return 0;
}

 ```
<img width="1016" height="293" alt="image" src="https://github.com/user-attachments/assets/b8cd2f5d-6502-4e69-8887-2418a737b8b5" />

**3. Justificación**

Cree un destructor para las estadísticas del personaje y luego cree una copia que toma los mismos valores de heroe pero no la dirección, luego cambie uno de las estadísticas para verificar que no se sobreescribieran las del heroe y además llamé la función imprimir para que si apareciera.





