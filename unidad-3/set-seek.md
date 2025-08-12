# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad 01
Toma de nota actividad

´´´ 
#include <iostream>
#include <iostream>

int sum(int a, int b)
{
    return a + b;
}

int main()
{
    int a = 5;
    int b = 7;
    std::cout << "La suma de " << a << " y " << b << " es " << sum(a, b) << "\n";  //Para acceder al objeto de salida y se le va a enviar la suma del valor de a, más el valor del valor b y se manda la función de la suma
}

#### Reflexión
**1. ¿Para qué sirven los breakpoints?**
Los breakpoints sirven para marcar una parte del código y además para ejecutarlo hasta una parte específica, funciona para verificar por partes qué sección es correcta en lugar de obtener un error al depurar todo. Lo coloque porque quiero enfocarme en un punto del programa y quiero detenerme en ese punto antes de ejcutar esa línea de código y según eso tomo decisiones.

**¿Para qué se usa la ventana de depuración Autos?**
La depuración en autos sirve para que todas las variables locales que se van declarando y definiendo a medida que el programa se va procesando.

### Actividad 02
---
*Toma de nota*

  **La función modificar** por valor toma el valor de a y ese valor se guarda en n que se convierte en una variable local de la función, cunado se salga de ahí se va a destruir. En la nueva variable se guarda un a copia dice lo que tenía en a, al salir de la función la variable se debería de destruir.

  **La función modificar por referencia** Hablar de n o hablar de b es hablar de la misma posición de memoria, es como un  apodo (Ej. Nicolás y Nico). No le paso el valor de la variable si no la referencia de la variable que sería la propia variable. 

  **La función modificar por puntero** Recibe una dirección de una variable, para modificar la variable de a cual yo recibí la dirección tengo que usar asterisco. Es como si estubiese modificando directamente la variable b. Se pasa un alias desde la variable original y a través de la dirección de la variable y un puntero modifico la variable original.

---

Análisis de código

#include <iostream>

using namespace std;

// Función que modifica el parámetro pasado por valor
void modificarPorValor(int n) {
    cout << "Dentro de modificarPorValor, valor inicial: " << n << endl;
    n += 5;
    cout << "Dentro de modificarPorValor, valor modificado: " << n << endl;
}

// Función que modifica el parámetro pasado por referencia
void modificarPorReferencia(int &n) {
    cout << "Dentro de modificarPorReferencia, valor inicial: " << n << endl;
    n += 5;
    cout << "Dentro de modificarPorReferencia, valor modificado: " << n << endl;
}

// Función que modifica el parámetro utilizando punteros
void modificarPorPuntero(int *n) {
    cout << "Dentro de modificarPorPuntero, valor inicial: " << *n << endl;
    *n += 5;
    cout << "Dentro de modificarPorPuntero, valor modificado: " << *n << endl;
}

int main() {
    int a = 10;
    int b = 10;
    int c = 10;

    cout << "Valor inicial de a (paso por valor): " << a << endl;
    cout << "Valor inicial de b (paso por referencia): " << b << endl;
    cout << "Valor inicial de c (paso por puntero): " << c << endl;

    cout << "\nLlamando a modificarPorValor(a)..." << endl;
    modificarPorValor(a);
    cout << "Después de modificarPorValor, valor de a: " << a << endl;

    cout << "\nLlamando a modificarPorReferencia(b)..." << endl;
    modificarPorReferencia(b);
    cout << "Después de modificarPorReferencia, valor de b: " << b << endl;

    cout << "\nLlamando a modificarPorPuntero(&c)..." << endl;
    modificarPorPuntero(&c);
    cout << "Después de modificarPorPuntero, valor de c: " << c << endl;

    return 0;
}

**1. Predicción: antes de ejecutar el programa, predice la salida de cada función y explica el resultado.**
Declaramos las variables como enteros, luego mandamos al objeto unos valores. Para A aparecerá un 10, luego el 10 se aumentará a 15 y al realizar la operación A debería de tener el valor de 15. **Esto es erroneo porque en realidad se crea una copia del valor de a en otra variable y al salir de la función se destruye por lo que queda con el valor inicial que era 0**

 Para B, creo que el valor de B no se va a modificar porque estoy pasando el valor de B así que debería de ser algo similar a A. No creo que sea exactamente lo mismo porque tiene el & pero no se me ocurre qué más podría ser, a lo mejor no se destruye la variable n. **Es erroneo porque B si se modifica, es como si usara un apodo para referirme al mismo.**
 
  Creo que a la función levoy a pasar la dirección de c y estoy creando una variable nueva donde se guardará el valor de c y a través del puntero voy a modificar el valor. **La hipótesis es correcta**, cuando llamo un puntero le estoy pasando la dirección e la variable que estoy guardando en n, aunque esta desaparezca yo modifique la original a través de un puntero. Es lo que trabajamos en la actividad anterior.

**2. ¿Qué diferencias observas en el comportamiento de a, b y c tras cada llamada?**
La función modificar por valor toma el valor de a y ese valor se guarda en n que se convierte en una variable local de la función, cunado se salga de ahí se va a destruir.

**3. ¿Por qué ocurre esta diferencia?**

#### Reflexión
Crea un proyecto de consola en Visual Studio. Implementa swapPorValor(int a, int b)

**Código**

Muestra los resultados de las pruebas realizadas en la función main().
