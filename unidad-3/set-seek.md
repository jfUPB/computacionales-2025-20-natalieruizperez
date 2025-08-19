# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad 01
Toma de nota actividad

``` c++
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
```

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
**Análisis de código**

```c++
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
```

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

Hay que hacer 3, intentar hacerlo modificando el código que ya tenemos, hay que cambiar los mensajes que se van a imprimir y las funciones.

**swapPorValor(int a, int b) - Que a tenga el valor de b y b el valor de a**

```c++
// Función que modifica el parámetro pasado por valor
void swapPorValor(int a, int b) {
    cout << "Dentro de swapPorValor. a,b: " << a << ',' << b << endl;

    int tmp = b;       //Variable temporal en donde se guarda el valor de b
    b = a;            // b toma el valor de a
    a = tmp;          // a toma el valor de b
 
    //No cambia los valores originales porque son copias
    cout << "Dentro de swapPorValor valores modificados. a,b: " << a << ',' << b << endl;
}
```

**swapPorReferencia(int &a, int &b)** - Estoy creando alias para las dos variables

```c++
// Función que modifica el parámetro pasado por referencia
void modificarPorReferencia(int &a, int &b) {
    cout << "Dentro de modificarPorReferencia, valores iniciales. a,b : " << a << ',' << b << endl;

    int tmp = b;    // Variable temporal en donde se guarda el valor de b
    b = a;         // b toma el valor de a
    a = tmp;       // a toma el valor de b

    //Se cambian los valores originales de a y b porque son apodos para referirme a lo mismo
    cout << "Dentro de modificarPorReferencia, valores modificados. a,b : " << a << ',' << b << endl;
}
```

**swapPorPuntero(int *a, int *b)** - Estoy manipulando las variables a través de sus direcciones.

```c++
// Función que modifica el parámetro utilizando punteros
// Tiene que dar 10, 20
void modificarPorPuntero(int* a, int* b) {
    cout << "Dentro de modificarPorPuntero,valores iniciales. a,b : " << *a << ',' << *b << endl;

    int tmp = *b;   // Variable temporal que guarda el valor apuntado por b
    *b = *a;         /// El valor apuntado por b toma el valor apuntado por a
    *a = tmp;        // El valor apuntado por a toma el valor de b
    
    // Se cambian los valores originales de a y b porque modifico lo que apuntan los punteros
    cout << "Dentro de modificarPorPuntero, valores modificados. a,b : " << *a << ',' << *b << endl;
}
```

**Main**

```c++
int main() {
    int a = 10;
    int b = 20;
    int c = 10;

    cout << "Valor inicial de a (paso por valor): " << a << endl;
    cout << "Valor inicial de b (paso por referencia): " << b << endl;
    cout << "Valor inicial de c (paso por puntero): " << c << endl;

    cout << "\nLlamando a swapPorValor(a,b)..." << endl;
    swapPorValor(a, b);
    cout << "Después de swapPorValor, valores de a,b: " << a << ',' << b << endl;

    cout << "\nLlamando a modificarPorReferencia(a,b)..." << endl;
    modificarPorReferencia(a,b);
    cout << "Después de modificarPorReferencia, valores de a,b: " << a << ',' << b << endl;

    cout << "\nLlamando a modificarPorPuntero(&a, &b)..." << endl;
    modificarPorPuntero(&a, &b);
    cout << "Después de modificarPorPuntero,  valores de a,b: " << a << ',' << b << endl;

    return 0;
}
```

---
### Actividad integradora de investigación

**Predicción**
```c++
#include <iostream>

int contador_global = 100;                //Tengo una variable global que se puede usar en las demas funciones

void ejecutarContador() {                //Función que no devuelve ningún valor
    static int contador_estatico = 0;    // Inicializo el contador estático
    contador_estatico++;                 // El contador aumenta cada vez que se llama esta funcion

    // De esta funcion muestra el valor del contador estático
    std::cout << "  -> Llamada a ejecutarContador. Valor de contador_estatico: " << contador_estatico << std::endl;
}

void sumaPorValor(int a) {            //Declaro una variable en la función
    a = a + 10;                       // Al valor actual de a le sumo 10 y su nuevo valor se guarda en a

    // Esta copia de a debe de tener el valor de 30 pero no modifica la variable original
    // Imprime el valor de a dentro de esta función
    std::cout << "  -> Dentro de sumaPorValor, 'a' ahora es: " << a << std::endl;           
}

void sumaPorReferencia(int& a) {     //Declaro un alias en la función
    a = a + 10;                      // Al valor actual de a le sumo 10 y su nuevo valor se guarda en a

    // Como es por referencia el valor original debió de pasar de 20 a 30
    // Imprime el valor de a dentro de esta función
    std::cout << "  -> Dentro de sumaPorReferencia, 'a' ahora es: " << a << std::endl;
}

void sumaPorPuntero(int* a) {       //Declaro una variable en la función para sumar por puntero
    *a = *a + 10;                   // Apunto al valor actual de a, le sumo 10 y su nuevo valor apunta a a

    //  Imprime el valor de a dentro de esta función
    std::cout << "  -> Dentro de sumaPorPuntero, '*a' ahora es: " << *a << std::endl;
}

int main() {
    // Declaro variables
    int val_A = 20;
    int val_B = 20;
    int val_C = 20;

    std::cout << "--- Experimento con paso de parámetros ---" << std::endl;
    std::cout << "Valor inicial de val_A: " << val_A << std::endl;           //El valor inicial de A es 20
    sumaPorValor(val_A);                  
    std::cout << "Valor final de val_A: " << val_A << std::endl << std::endl;   // A debe de seguir siendo 20

    std::cout << "Valor inicial de val_B: " << val_B << std::endl;      // El valor inicial de B es 20
    sumaPorReferencia(val_B); 
    std::cout << "Valor final de val_B: " << val_B << std::endl << std::endl;  // El nuevo valor de B debe de ser 30

    std::cout << "Valor inicial de val_C: " << val_C << std::endl;
    sumaPorPuntero(&val_C);               // Accedo a la dirección de c
    std::cout << "Valor final de val_C: " << val_C << std::endl << std::endl;  // El nuevo valor de c es 30

    std::cout << "--- Experimento con variables estáticas ---" << std::endl;
    ejecutarContador();      // El contador estático es 1
    ejecutarContador();      // El contador estático es 1 
    ejecutarContador();      // El contador estático es 1

    return 0;
}
```
Al ejecutar el código me di cuenta que tuve un error en la función ejecutarContador. Cuando hice la predicción asumí que el contador se resetearía cada vez, ya que la línea static int contador_estatico = 0; está al inicio de la función, pero no me parecía lógico porque cada vez que se llamara no se actualizaría el valor. Al revisar las actividades entendí que, al ser una variable static, se inicializa solo una vez al ejecutar la función por primera vez, es por esto que contador estático tiene que aumentar cada vez que se llama la función ejecutarContador();.

  También revisé las notas para ver cómo explicar de forma diferente esta parte "// Apunto al valor actual de a, le sumo 10 y su nuevo valor apunta a a" porque no me parece una explicación clara. Una mejor forma de decirlo sería "Accedo al valor apuntado por el puntero a, le sumo 10, y se guarda el nuevo valor en esa misma dirección". Además aquí sumaPorPuntero(&val_C); // Accedo a la dirección de c, me faltó decir que modifico el valor con el puntero.
  
**Mapa de memoria conceptual de este programa justo antes de que main finalice.**
  <img width="384" height="347" alt="image" src="https://github.com/user-attachments/assets/84a571b7-6d3e-4fcc-87d9-0bec0de15a9f" />

  No puse el parámetro a de la función SumaPorValor porque la instrucción dice que debo de poner en el mapa de memoria lo que está antes de que el main finalice y eso hace parte de otra función. Además ese valor a solo existiría dentro de la función SumaPorValor. El parámetro a es una copia que se destruye cuando se sale de la función.

**Verificación y análisis**
<img width="1480" height="512" alt="image" src="https://github.com/user-attachments/assets/52536644-174f-4130-b021-d24ee78be809" />

Se cumple la predicción, el valor inicial es el mismo que el final porque en la función SumaPorValor se crea una copia de la variable original y como se modifica dicha copia la variable original no se ve afectada.

<img width="1515" height="521" alt="image" src="https://github.com/user-attachments/assets/9934c4e8-cb63-4f2f-9687-503259a1ab22" />

Se cumple la predicción, el valor inicial es diferente al del final porque en la función SumaPorReferencia la variable de la función es un apodo de la variable original, por lo que al modificar ese apodo se modifica la del principio.

<img width="1565" height="513" alt="image" src="https://github.com/user-attachments/assets/ddc70c8b-09c5-4329-a725-5c663851da12" />

Se cumple la predicción, el valor incial es diferente al del final porque en la función SumaPorPuntero se accede a la variable original a través del puntero y se modifica usando su dirección.

<img width="1682" height="528" alt="image" src="https://github.com/user-attachments/assets/6fd9f226-c705-48f3-af8b-887de4addb01" />

Aquí fue donde falló  mi predicción porque dije que cada vez que se llamaba la función ejecutarContador, el resultado iba a ser 1. La variable contador_estatico como es estática el programa inicializa el valor solo la primera vez que corre la función. A diferencia con una variable local normal, la estática recuerda el valor que tuvo la última vez que se usó. Hipotéticamente hablando si en el programa el contador no hubiese sido estático, el resultado hubiese sido que cada vez que se llama la función se sobreescribe la variable y el resultado sería el que predije.



