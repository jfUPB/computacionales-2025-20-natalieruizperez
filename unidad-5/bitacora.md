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
  
<a name="expf"></a>
### Experimento fallido

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
<a name="pregu"></a>

### Preguntas que me surgieron luego de analizar el código:
1. ¿Cómo a pesar de tener los mismos nombres hacen acciones diferentes? ¿El programa cómo lo entiende?
2. ¿Por qué uso "fig" antes de dibujar? ¿Cómo se relaciona la clase abstracta de dibujar con figura? ¿El programa cómo sabe cúal ejecutar?
3. Cuando la  clase figura toma un nombre ¿Ese nombre es el mismo que el de los strings public y private creado anteriormente? ¿Si es diferente el programa cómo sabe?

Creo que estas preguntas las podré responder al analizar el código entonces iré a c#. Al correr el código veo que efectivamente a pesar de que los métodos se llamen dibujar cada uno hace algo diferente
<img width="1048" height="706" alt="image" src="https://github.com/user-attachments/assets/ac50a1a6-665d-4764-9b75-f605c9632553" />

Voy a observar con los brakpoints que es lo que sucede a nivel de memoria. Dado que c# esconde lo que sucede voy a pedirle a la ia que lo convierta a un código en c++ para analizar la memoria correctamente.


<img width="901" height="288" alt="image" src="https://github.com/user-attachments/assets/704fe03a-3b9f-4a04-90ce-79f6e1652a32" />

<a name="cod"></a>
Código de análisis

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
<a name="ana"></a>
Análisis de código

Una vez convertido el código voy a poner breakpoints para analizar la memoria, pero primero verificar que el código funcione correctamente.

<img width="1493" height="718" alt="image" src="https://github.com/user-attachments/assets/662f9e94-1080-4b92-ad55-f685e98a480a" />

Ahora a analizar el stack. Veo que en las variables locales está el nuevoNombre que lo puedo ubicar en el programa sin problema, pero hay una variable llamada **this** la cual no veo en el códgio.

<a name="preg0"></a>
Preguntas

**¿Qué es esa variable this que crea el código y de qué se encarga?**

Sin this, el método setNombre() no sabría en qué objeto debe modificar la variable nombre. Gracias a this, el compilador resuelve que nombre pertenece al objeto actual. Cuando se a un método como setNombre(), this contiene la dirección de memoria del objeto que está invocando ese método.

<a name="con0"></a>
En conclusión, this no es una variable que aparezca de forma literal en el programa pero es fundamental ya que ella alberga la dirección de memoria del objeto para que el programa pueda saber a qué me refiero.

<img width="934" height="628" alt="Captura de pantalla 2025-09-16 091420" src="https://github.com/user-attachments/assets/69603368-a523-4776-bc64-61504c027671" />

el valor de this es 0x0000011914447a20, que es la dirección de memoria del objeto Figura en construcción y al abrirlo veo que hay una tabla __vfptr pero no sé la dirección de memoria a qué corresponde, su dirección es la siguiente 0x00007ff76c4646b8. Voy a seguir observando el código en busca de que objeto tiene esa dirección.

<img width="937" height="544" alt="image" src="https://github.com/user-attachments/assets/f2196b32-76e2-4f48-a43b-7a136bb6ff34" />

Encontré en qué la tabla hace referencia a la figura porque es la clase padre y la que se construye primero. Ahora tengo las siguientes preguntas:

<a name="preg1"></a>
### Preguntas de los nombres en el depurador

**1. ¿Qué es exactamente un _vfptr? ¿Es lo mismo que una vtable?**

Las siglas _vfptr son por virtual function pointer y es un puntero implícito que todo objeto de una clase con funciones virtuales contiene. Apunta a la vtable de su clase. Es una tabla de punteros a funciones virtuales. Cada clase con métodos virtuales tiene su propia vtable, que almacena las direcciones de las implementaciones de esas funciones. 

<a name="con1"></a>
En conclusión _vfptr es el puntero que apunta a la vtable. No son lo mismo pero se relacionan.

**2. ¿Por qué en la imagen hay una Figura con y sin corchetes? ¿Cúal es la diferencia?**

Los corchetes son para acceder a entradas específicas de la vtable, mientras que sin corchetes, se describe la vtable en general o la clase a la que pertenece. 

<img width="974" height="616" alt="image" src="https://github.com/user-attachments/assets/4cf408bb-5565-4cae-a4e5-69680ac42273" />

Veo que se ambas figuras, con y sin corchete tienen la misma drirección de memoria, esto es porque todos los objetos del mismo tipo comparten la misma vtable. 

  Ahora voy a analizar la creación de objetos, y observar qué sucede. Veo que se creo un elemento [0] ya que lo estoy ejecutando por partes.

  <img width="920" height="449" alt="image" src="https://github.com/user-attachments/assets/879e2243-e917-4ade-97d1-7edffe0c59e9" />

  El vector tiene la capacidad de 1 y parece que está compuesto por un puntero, un deleter que parece que es para borrar algo en específico
<img width="921" height="426" alt="image" src="https://github.com/user-attachments/assets/6229ad8e-b370-47e0-8211-1ff08278e5e8" />

Al abrir el puntero veo que tiene una referencia a la figura, en este caso el círculo, también tiene un puntero que apunta a la vtable y el nombre del objeto.

<img width="933" height="431" alt="image" src="https://github.com/user-attachments/assets/878fb43b-d877-48d2-a13e-2c4bf5ef63eb" />

Cuando abro el puntero veo que apunta a dos elementos y además estos tienen direcciones diferentes ¿Estas direcciones qué referencian? Luego de inspeccionar vi que esta referencia al círculo 0x00007ff73887149c, pero la otra que es 0x00007ff738871767 no sé qué referencia, voy a seguir analizando el código.

<img width="914" height="483" alt="image" src="https://github.com/user-attachments/assets/fa3718ce-6275-406e-a207-a30df808a6b6" />

Cuando abro círculo que es una entrada específica a la vtable, también que círculo contiene figura, esto es algo contraintuitivo porque círculo hereda a padre, pero es así porque círculo tienen los mismos parámentros que figura. Lo que quiere decir que así se implementa la herencia en c++

<img width="904" height="514" alt="image" src="https://github.com/user-attachments/assets/90ae5726-5b9e-439a-a704-9830b5406c0a" />

[Figura] tiene su nombre y también un puntero a la tabla, este puntero también apunta a dos elementos y veo que tiene la misma dirección que el círculo y la otra que desconozco.

<img width="894" height="527" alt="image" src="https://github.com/user-attachments/assets/cb087e7f-881c-4fdd-8425-504261c764d3" />

<a name="conc3"></a>
#### **Conclusión análisis creación de figuras**

Circulo es una extensión de Figura en memoria. Al heredar, la parte de Figura se convierte en el primer segmento de cualquier objeto Circulo. Esto explica por qué ambos comparten la misma dirección inicial y el mismo puntero _vfptr. Todas comparten la misma tabla de la clase Circulo. En este orden de ideas puedo pensar que el puntero y la vtable son un sistema de direcciones que le dice al programa específicamente qué dibujar.

<a name="preg2"></a>
### **Preguntas de la creación de objetos**

**1. ¿Qué es "push_back" y "vector<unique_ptr<Figura>>"? ¿Para qué sirven?**

El primero agrega un nuevo elemento al final de un vector y el otro es un vector que guarda punteros a objetos del tipo Figura.

**2. ¿El deleter qué borra?**

Es el mecanismo que se encarga de liberar automáticamente la memoria del objeto al que apunta el puntero, viene por defecto que viene con unique_ptr.

**3. ¿Por qué el puntero a punta dos elementos si por el momento solamente hay uno en el vector?**

Al consultar encontré que no son dos elementos, si no la vtable del círculo que contiene punteros, uno que se encarga de dibujar el círculo y el otro de borrarlo.

**4. ¿Por qué todos los elementos tienen un componente entre corchetes llamado vista sin formato?**

Es una herramienta del entorno de depuración para ver los detalles internos, es para poder inspeccionar objetos complejos.

<a name="ana2"></a>
Continuaré analizando el código y al hacerlo veo que ahora se creo la nueva figura rectángulo 

<img width="926" height="887" alt="image" src="https://github.com/user-attachments/assets/c149fce0-be51-4471-b74b-36fde11b7e17" />

Tiene los mismos componentes solo que sta vez en vez de círculo aparece rectángulo.

<img width="880" height="562" alt="image" src="https://github.com/user-attachments/assets/b00fa8e2-0fab-4fef-b144-76a4113eb675" />

Veo que también su puntero esta compuesto por dos y ya se por qué aunque sea un solo objeto. La dirección del rectángulo es 0x00007ff73887114a

<img width="914" height="608" alt="image" src="https://github.com/user-attachments/assets/298323ae-0b44-4cfc-9e91-0eef937af491" />

Al final se puede ver como se llaman a 3 elementos, uno sería el círculo, otro el rectángulo y después otro círculo.

<img width="921" height="737" alt="image" src="https://github.com/user-attachments/assets/4092a2db-3f85-45ce-ae42-2fb36ed8fabc" />

Veo que ambos círculos tiene la misma dirección de memoria.

<img width="921" height="662" alt="image" src="https://github.com/user-attachments/assets/b3540899-23e6-40d4-9285-2af2ca20522d" />

---
<a name="exp0"></a>
### Experimento

Como experimento voy a observar si es posibe hackear el programa en tiempo real. Lo primero que voy a hacer es copiar la dirección del rectángulo, esta es 0x00007ff66273114a y la del círculo que es 0x00007ff66273149c. Mi plan es poner en el rectángulo la dirección del círculo y observar qué sucede.


**Dirección de rectángulo**

<img width="921" height="544" alt="image" src="https://github.com/user-attachments/assets/7a921f52-010d-4168-8173-60bdf856976b" />

**Dirección de memoria del círculo**

<img width="921" height="544" alt="image" src="https://github.com/user-attachments/assets/34022025-2801-4552-8440-96a155d3bddd" />

Alias de fig que toma las referencias del otro grupo por asi decirlo
.
<img width="936" height="511" alt="image" src="https://github.com/user-attachments/assets/e28bc8bb-8725-4236-a3ef-feb679dfe41c" />

## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación

### Nota:

-Profundidad de la Indagación (5.0): Formulo preguntas que desmuestran síntesis conceptual y relaciono el diseño con memoria y sintaxis como se puede ver por ejemplo en estas [Preguntas](#preg0) donde dice "Gracias a this, el compilador resuelve que nombre pertenece al objeto actual." También hice más que se pueden encontrar en [Preguntas 1](#preg1), [Preguntas 2](#preg2) y [Preguntas al ver el código](#pregu).

-Calidad de la Experimentación (5.0): Hice dos experimentos, considero que ambos muy completos dado que el primero no involucraba unicamente polimorfismo si no también herencia y encapsulamiento como se puede ver en el [experimento 1](#cod). En el segundo experimento [Experimento 2](#exp0) modifiqué manualmente la dirección de memoria de un objeto Figura que originalmente era un Rectángulo, para que apuntara a la instancia de un Circulo. Lo que descubrí fue que, al ejecutar Dibujar(), el programa no dibujó el rectángulo, sino el círculo.

-Análisis y Reflexión (5.0): A lo largo de la bitácora definí que iba a hacer, después observé qué sucedía, lo analicé y finalmente hice una conclusión. Por ejemplo en esta parte me pregunto el por qué del diseño, hago una reflexión y finalmente una conclusión.

-Apropiación y Articulación de Conceptos (5.0):







> Criterio 1: Por ejemplo en el [experimento 1](#exp1) se nota que .... porque ...
