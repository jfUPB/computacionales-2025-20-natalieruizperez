# Bitácora de aprendizaje de la unidad 5

## 1.  **Diagnóstico inicial**

**1. ¿Qué es el encapsulamiento para ti? Describe una situación en la que te haya sido útil o donde hayas visto su importancia.**
El encapsulamiento para mí es cuando decido que tipo de acceso tiene un componente, este puede ser público, privado, etc. es muy importante porque así puedo controlar como manejo mis datos

**2. ¿Qué es la herencia? ¿Por qué un programador decidiría usarla? Da un ejemplo simple.**
La herencia se usa cuando quiero que una clase reciba los mismos parámetros que una clase padre. Tiene este nombre porque siempre hay una clase hija que hereda de una clase padre. Sirve para reutilizar código ya que la clase padre suele ser una base, de esta forma es posible mantener el programa más organizado.  

**3.¿Qué es el polimorfismo? Describe con tus palabras qué significa que un código sea “polimórfico”.**

El polimorfismo es cuando puedo darle a diferentes clases métodos con el mismo nombre, pero que hacen diferentes acciones según la clase. Este concepto me cuesta entenderlo porque a pesar de que lo vi en POO a la hora de implementarlo tiendo a confundirme.

## 2.  **La pregunta inicial**
¿Cómo funciona el polimorfismo a nivel de memoria? Puedo cambiar la dirección para que pasen otras cosas ¿Puedo hackear el programa en tiempo de ejecución? Hacer un análisis. Reinterpretamiento de casting es lo que muestra la ia 

## 3.  **Registro de exploración:** 

> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

Mi hipótesis es que cada vez que hago polimorfismo a pesar de que los métodos tienen el mismo nombre, estos tienen que funcionar a nivel de memoria de forma diferente para poder almacenar los datos. Mi propósito es entender  por qué es posible realizar polimorfismo y cómo se hace. Una vez comprendido el concepto quiero observar si es posible hackear el programa en tiempo de ejecución, por el momento pienso que sí pero no tengo muy claro cómo, quizás cambiando las direcciones en tiempo real, además quiero entender esto para qué serviría.

  Lo primero que voy a hacer es analizar el código de la actividad uno ya que está relacionada con polimorfismo pero antes voy a ver qué hace el código para entender qué hace antes de observar la parte de la memoria.

**Código**
```c#
using System;
using System.Collections.Generic;

public abstract class Figura               //Una clase abstracta que no puede heredar nada
{
    private string nombre;                //Variable privada que solo existe dentro de la clase

    public string Nombre                  //Una variable pública con el mismo nombre pero en mayúsculas que retorna el valor del nombre privado, parece que sirve como un puente
    {
        get { return nombre; }
        protected set { nombre = value; }
    }

    public Figura(string nombre)        //Una clase pública llamada figura que recibe un nombre. ¿Ese nombre será el mismo que el private string o uno diferente?
    {
        this.Nombre = nombre;
    }

    public abstract void Dibujar();    //Una clase abstracta para dibujar
}

public class Circulo : Figura                          //La clase círculo hereda la de figura por lo cuál
{
    public double Radio { get; private set; }

    public Circulo(double radio) : base("Círculo")   //Aquí me había perdido pero veo que está llamando la clase círculo y  como toma de base la de figura le asigna el nombre
    {
        this.Radio = radio;
    }

    public override void Dibujar()                  //Estoy tomando la clase abstracta de dibujar y le estoy diciendo que escriba eso
    {
        Console.WriteLine($"Dibujando un {Nombre} de radio {Radio}.");
    }
}

public class Rectangulo : Figura                 //Rectángulo hereda figura
{
    public double Base { get; private set; }
    public double Altura { get; private set; }

    public Rectangulo(double b, double h) : base("Rectángulo")   //Aquí pongo los parámetros
    {
        this.Base = b;
        this.Altura = h;
    }

    public override void Dibujar()              //Vuelvo a hacer override en dibujar pero me pregunto ¿Cómo a pesar de tener los mismos nombres hacen acciones diferentes?
    {
        Console.WriteLine($"Dibujando un {Nombre} de {Base}x{Altura}.");
    }
}

public class Programa                             
{
    public static void Main()
    {
        List<Figura> misFiguras = new List<Figura>();          // Creo una lista para mis figuras

        misFiguras.Add(new Circulo(5.0));                    //Aquí estoy creando los objetos y seteando los parámetros para cada una en cuanto radio, altura o base
        misFiguras.Add(new Rectangulo(4.0, 6.0));
        misFiguras.Add(new Circulo(10.0));

        foreach (Figura fig in misFiguras)                // Para cada una de las figuras en mis listas llamo a dibujar para que escriban 
        {
            fig.Dibujar();
        }
    }
}
```

**Preguntas que me surgieron luego de analizar el código:**
1. ¿Cómo a pesar de tener los mismos nombres hacen acciones diferentes? ¿El programa cómo lo entiende?
2. ¿Por qué uso "fig" antes de dibujar? ¿Cómo se relaciona la clase abstracta de dibujar con figura? ¿El programa cómo sabe cúal ejecutar?
3. Cuando la  clase figura toma un nombre ¿Ese nombre es el mismo que el de los strings public y private creado anteriormente? ¿Si es diferente el programa cómo sabe?

Creo que estas preguntas las podré responder al analizar el código entonces iré a c#. Al correr el código veo que efectivamente a pesar de que los métodos se llamen dibujar cada uno hace algo diferente
<img width="1048" height="706" alt="image" src="https://github.com/user-attachments/assets/ac50a1a6-665d-4764-9b75-f605c9632553" />

Voy a observar con los brakpoints que es lo que sucede a nivel de memoria. Dado que c# esconde lo que sucede voy a pedirle a la ia que lo convierta a un código en c++ para analizar la memoria correctamente.
<img width="901" height="288" alt="image" src="https://github.com/user-attachments/assets/704fe03a-3b9f-4a04-90ce-79f6e1652a32" />

**Código c++**

```c++
#include <iostream>
#include <vector>
#include <memory>  // Para smart pointers
#include <string>

using namespace std;

// Clase abstracta Figura
class Figura {
private:
    string nombre;  // Variable privada

protected:
    void setNombre(const string& nuevoNombre) {
        nombre = nuevoNombre;
    }

public:
    Figura(const string& nombre) {
        setNombre(nombre);
    }

    string getNombre() const {
        return nombre;
    }

    virtual void Dibujar() const = 0; // Método virtual puro (abstracto)

    virtual ~Figura() {} // Destructor virtual necesario para polimorfismo
};

// Clase Circulo que hereda de Figura
class Circulo : public Figura {
private:
    double radio;

public:
    Circulo(double r) : Figura("Círculo"), radio(r) {}

    double getRadio() const {
        return radio;
    }

    void Dibujar() const override {
        cout << "Dibujando un " << getNombre() << " de radio " << radio << "." << endl;
    }
};

// Clase Rectangulo que hereda de Figura
class Rectangulo : public Figura {
private:
    double base;
    double altura;

public:
    Rectangulo(double b, double h) : Figura("Rectángulo"), base(b), altura(h) {}

    double getBase() const {
        return base;
    }

    double getAltura() const {
        return altura;
    }

    void Dibujar() const override {
        cout << "Dibujando un " << getNombre() << " de " << base << "x" << altura << "." << endl;
    }
};

// Función principal
int main() {
    vector<unique_ptr<Figura>> misFiguras;

    // Creamos las figuras con smart pointers
    misFiguras.push_back(make_unique<Circulo>(5.0));
    misFiguras.push_back(make_unique<Rectangulo>(4.0, 6.0));
    misFiguras.push_back(make_unique<Circulo>(10.0));

    // Llamamos a Dibujar en cada una
    for (const auto& fig : misFiguras) {
        fig->Dibujar();
    }



    return 0;
}
```
Una vez convertido el código voy a poner breakpoints para analizar la memoria, pero primero verificar que el código funcione correctamente.

<img width="1493" height="718" alt="image" src="https://github.com/user-attachments/assets/662f9e94-1080-4b92-ad55-f685e98a480a" />

Ahora a analizar el stack. Veo que en las variables locales está el nuevoNombre que lo puedo ubicar en el programa sin problema, pero hay una variable llamada **this** la cual no veo en el códgio.

**¿Qué es esa variable this que crea el código y de qué se encarga?**

Sin this, el método setNombre() no sabría en qué objeto debe modificar la variable nombre. Gracias a this, el compilador resuelve que nombre pertenece al objeto actual. Cuando se a un método como setNombre(), this contiene la dirección de memoria del objeto que está invocando ese método.

En conclusión, this no es una variable que aparezca de forma literal en el programa pero es fundamental ya que ella alberga la dirección de memoria del objeto para que el programa pueda saber a qué me refiero.

<img width="934" height="628" alt="Captura de pantalla 2025-09-16 091420" src="https://github.com/user-attachments/assets/69603368-a523-4776-bc64-61504c027671" />

el valor de this es 0x0000011914447a20, que es la dirección de memoria del objeto Figura en construcción y al abrirlo veo que hay una tabla __vfptr pero no sé la dirección de memoria a qué corresponde, su dirección es la siguiente 0x00007ff76c4646b8. Voy a seguir observando el código en busca de que objeto tiene esa dirección.

<img width="937" height="544" alt="image" src="https://github.com/user-attachments/assets/f2196b32-76e2-4f48-a43b-7a136bb6ff34" />

Encontré en qué la tabla hace referencia a la figura porque es la clase padre y la que se construye primero. Ahora tengo las siguientes preguntas:

**1. ¿Qué es exactamente un _vfptr? ¿Es lo mismo que una vtable?**

Las siglas _vfptr son por virtual function pointer y es un puntero implícito que todo objeto de una clase con funciones virtuales contiene. Apunta a la vtable de su clase. Es una tabla de punteros a funciones virtuales. Cada clase con métodos virtuales tiene su propia vtable, que almacena las direcciones de las implementaciones de esas funciones. 

En conclusión _vfptr es el puntero que apunta a la vtable. No son lo mismo pero se relacionan.

**2. ¿Por qué en la imagen hay una Figura con y sin corchetes? ¿Cúal es la diferencia?**

Los corchetes son para acceder a entradas específicas de la vtable, mientras que sin corchetes, se describe la vtable en general o la clase a la que pertenece.

---
### Experimento

Como experimento voy a observar si es posibe hackear el programa en tiempo real. Lo primero que voy a hacer es copiar la dirección del rectángulo, esta es 0x00007ff66273114a y la del círculo que es 0x00007ff66273149c. Mi plan es poner en el rectángulo la dirección del círculo y observar qué sucede.

**Dirección de rectángulo**

<img width="921" height="544" alt="image" src="https://github.com/user-attachments/assets/7a921f52-010d-4168-8173-60bdf856976b" />

**Dirección de memoria del círculo**

<img width="921" height="544" alt="image" src="https://github.com/user-attachments/assets/34022025-2801-4552-8440-96a155d3bddd" />

Alias de fig que toma las referencias del otro grupo por asi decirlo.
<img width="936" height="511" alt="image" src="https://github.com/user-attachments/assets/e28bc8bb-8725-4236-a3ef-feb679dfe41c" />









## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
