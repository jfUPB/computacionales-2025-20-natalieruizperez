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



## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
