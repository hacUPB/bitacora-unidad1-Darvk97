# Sesión 1
## Actividad 1

- ¿Para qué sirven los breakpoints?

R: Los breakpoints sirven para detener la ejecución del programa en una línea específica. Esto permite revisar qué está haciendo el programa y observar los valores de las variables mientras se ejecuta.

- ¿Para qué se usa la ventana de depuración Autos?

R: La ventana Autos sirve para mostrar las variables que están relacionadas con la línea de código que se está ejecutando. Permite observar sus valores y cómo van cambiando durante la depuración.

## Actividad 2

- ¿Cuál es la predicción de la salida de cada función?

R: 1. modificarPorValor recibe una copia de a, por lo que dentro de la función el valor pasa de 10 a 15, pero a sigue siendo 10 después de la llamada.

2. modificarPorReferencia recibe una referencia a b, por lo que dentro de la función pasa de 10 a 15 y b también queda en 15 después de la llamada.

3. modificarPorPuntero recibe la dirección de c, por lo que puede modificar directamente su valor. Dentro de la función pasa de 10 a 15 y c queda en 15.

- ¿Qué diferencias observas en el comportamiento de a, b y c tras cada llamada?

R: a permanece en 10 porque se pasó por valor. b queda en 15 porque se pasó por referencia y c queda en 15 porque se modificó mediante un puntero.

- ¿Por qué ocurre esta diferencia?

R: Ocurre porque al pasar una variable por valor se crea una copia. En cambio, al pasarla por referencia se trabaja directamente con la variable original. Con un puntero también se puede modificar la variable original porque se utiliza su dirección de memoria.

- ¿Qué ocurre con modificarPorValor?

R: La función recibe una copia de a. Al sumar 5, la copia cambia de 10 a 15, pero la variable original a sigue teniendo el valor 10.

- ¿Qué ocurre con modificarPorReferencia?

R: n es una referencia a b, por lo que cuando se le suman 5 unidades se modifica directamente b. Por eso después de la función b vale 15.

- ¿Qué ocurre con modificarPorPuntero?

R: Se pasa la dirección de c usando &c. Dentro de la función se utiliza *n para acceder al valor almacenado en esa dirección. Al sumarle 5, se modifica directamente c.

### Reflexión final:

```asm
swapPorValor
void swapPorValor(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
}
```

R: Esta función intercambia las copias de los valores, pero no modifica las variables originales de main.

```asm
swapPorReferencia
void swapPorReferencia(int &a, int &b) {
    int temp = a;
    a = b;
    b = temp;
}
```

R: Esta función intercambia directamente los valores de las variables originales porque recibe referencias.

```asm
swapPorPuntero
void swapPorPuntero(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

R: Esta función recibe las direcciones de las variables y utiliza * para acceder a sus valores y poder intercambiarlos.

```asm
Programa
#include <iostream>
using namespace std;

void swapPorValor(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
}

void swapPorReferencia(int &a, int &b) {
    int temp = a;
    a = b;
    b = temp;
}

void swapPorPuntero(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int a = 5;
    int b = 10;

    cout << "Valores iniciales: a = " << a << ", b = " << b << endl;

    swapPorValor(a, b);
    cout << "Después de swapPorValor: a = " << a << ", b = " << b << endl;

    swapPorReferencia(a, b);
    cout << "Después de swapPorReferencia: a = " << a << ", b = " << b << endl;

    swapPorPuntero(&a, &b);
    cout << "Después de swapPorPuntero: a = " << a << ", b = " << b << endl;

    return 0;
}
```

### Resultados de las pruebas

R: 1. Los valores iniciales fueron a = 5 y b = 10.

2. Después de swapPorValor, los valores siguen siendo a = 5 y b = 10, porque la función solamente modificó las copias.

3. Después de swapPorReferencia, los valores quedaron a = 10 y b = 5.

4. Después de swapPorPuntero, los valores volvieron a quedar a = 5 y b = 10.

5. Esto demuestra que el paso por valor no modifica las variables originales, mientras que la referencia y el puntero sí pueden hacerlo.

# Sesión 2
## Actividad 3

- ¿En qué segmentos de memoria se organiza un programa en C++?

R: Un programa en C++ se puede dividir principalmente en el segmento de código, las variables globales y estáticas, el Heap y el Stack.

- ¿Qué contiene el segmento de código?

R: Contiene las instrucciones del programa y las funciones que se ejecutan, como main(), suma() y crearArrayHeap().

- ¿Dónde se almacenan las variables globales y estáticas?

R: Se almacenan en la zona de memoria destinada a datos globales y estáticos. Estas variables normalmente permanecen durante toda la ejecución del programa.

- ¿Qué es el Heap?

R: Es una zona de memoria utilizada para reservar memoria dinámicamente durante la ejecución del programa. En C++ se puede utilizar new para reservar memoria y delete para liberarla.

- ¿Qué es el Stack?

R: Es una zona de memoria donde normalmente se almacenan las variables locales y la información relacionada con las llamadas a funciones. Su manejo es automático.

- ¿Dónde se encuentra la variable a de main?

R: La variable a es una variable local, por lo que se encuentra en el Stack.

- ¿Dónde se encuentra global_inicializada?

R: Se encuentra en la zona de datos globales y estáticos.

- ¿Dónde se encuentra var_estatica?

R: Se encuentra en la zona de variables estáticas y permanece durante toda la ejecución del programa.

- ¿Dónde se encuentra arrayHeap?

R: El arreglo creado con new se encuentra en el Heap. La variable puntero arrayHeap que contiene su dirección es una variable local y se encuentra en el Stack.

- ¿Dónde se encuentran las funciones?

R: Las instrucciones de las funciones se encuentran en el segmento de código.

- ¿Dónde se encuentra el mensaje "Hola, memoria de solo lectura"?

R: El texto del mensaje se encuentra en una zona de memoria de solo lectura, mientras que el puntero mensaje_ro pertenece a los datos globales.

## Mapa de memoria

```asm
+--------------------------------+
|        SEGMENTO DE CÓDIGO      |
|                                |
| main()                         |
| suma()                         |
| crearArrayHeap()               |
| funcionConStatic()             |
+--------------------------------+
|    DATOS GLOBALES/ESTÁTICOS    |
|                                |
| global_inicializada             |
| global_no_inicializada          |
| var_estatica                    |
| mensaje_ro (puntero)            |
+--------------------------------+
|              HEAP              |
|                                |
| arreglo creado con new         |
| arrayHeap[0] ... arrayHeap[9]  |
+--------------------------------+
|             STACK              |
|                                |
| a                              |
| b                              |
| c                              |
| tamArray                       |
| arrayHeap (puntero)            |
| variables locales              |
+--------------------------------+
```

## Actividad 4

### Experimento 1: modificar el segmento de texto

- ¿Qué ocurre?

R: El programa normalmente se detiene con un error de acceso a memoria o se produce un crash.

- ¿Por qué?

R: Porque el programa intenta modificar la dirección donde comienza main, que pertenece al segmento de código. Esta memoria normalmente está protegida contra escritura, por lo que el sistema operativo impide modificarla.

### Experimento 4: modificar la variable local estática

- ¿Qué ocurre? ¿Por qué?

R: El programa no compila porque var_estatica solamente existe dentro de funcionConStatic(). Aunque sea estática y permanezca en memoria durante todo el programa, su alcance sigue siendo solamente dentro de la función.

- ¿Qué pasa con las variables cada vez que entras y sales de la función?

R: Una variable local normal se crea cuando se entra a la función y deja de existir cuando se sale de ella.

- ¿Qué pasa con las variables locales estáticas?

R: Una variable local estática se crea una sola vez y conserva su valor entre las diferentes llamadas a la función. No se destruye cada vez que se sale de la función.

### Experimento 5: variable local estática vs no estática

- ¿Qué ocurre? ¿Por qué?

R: var_no_estatica siempre muestra 100 porque se crea nuevamente cada vez que se llama a la función. var_estatica comienza en 100 y aumenta en cada llamada, por lo que muestra 100, 101, 102, 103 y 104.

- ¿Se observa alguna diferencia entre las variables locales estáticas y no estáticas?

R: Sí. La variable no estática comienza nuevamente en 100 en cada llamada, mientras que la variable estática conserva el valor que tenía de la llamada anterior.

- ¿Qué pasa con las variables cada vez que se entra y sale de la función?

R: La variable local normal se crea y se destruye en cada llamada. La variable estática permanece almacenada durante toda la ejecución del programa.

### Experimento 6: modificar el segmento de Heap

- ¿Qué ocurre? ¿Por qué?

R: Después de ejecutar delete[] arrayHeap, la memoria que ocupaba el arreglo deja de estar reservada para el programa. Al intentar acceder después con arrayHeap[0], se está utilizando un puntero que ya no apunta a memoria válida. Esto produce un comportamiento indefinido.

- ¿Qué diferencias notas entre el Heap y el Stack?

R: El Stack se administra automáticamente y las variables locales se destruyen al salir de su alcance. El Heap se utiliza para memoria dinámica y en C++ normalmente debemos liberar la memoria manualmente.

- ¿Qué consecuencias tendría no liberar la memoria reservada con new?

R: Se produciría una fuga de memoria. La memoria seguiría ocupada aunque ya no se esté utilizando, y si esto ocurre muchas veces el programa podría consumir cada vez más memoria.

- ¿Por qué es importante usar delete[] para un arreglo?

R: Porque el arreglo fue creado utilizando new[]. delete[] es la forma correcta de liberar la memoria reservada para ese arreglo.

## Actividad 5

```asm
Programa en C++
#include <iostream>
#include <string>
using namespace std;

class Punto {
public:
    string name;
    int x;
    int y;

    Punto(string _name, int _x, int _y) : name(_name), x(_x), y(_y) {
        cout << "Constructor: Punto " << name
             << " (" << x << ", " << y << ") creado." << endl;
    }

    ~Punto() {
        cout << "Destructor: Punto " << name
             << "(" << x << ", " << y << ") destruido." << endl;
    }

    void imprimir() {
        cout << "Punto " << name << "(" << x << ", " << y << ")" << endl;
    }
};

int main() {
    Punto original("original", 70, 80);
    original.imprimir();

    Punto* p = &original;

    Punto copia = original;

    copia.name = "copia";
    copia.x = 100;
    copia.y = 200;

    copia.imprimir();
    original.imprimir();

    p->name = "p";
    p->x = 300;
    p->y = 400;

    p->imprimir();
    original.imprimir();

    return 0;
}
```

- Explica qué ocurre al copiar un objeto en C++ y en C#. ¿Qué diferencias encuentras?

R: 1. En C++, al hacer Punto copia = original, se crea un nuevo objeto con una copia de los datos de original. Por eso los cambios realizados en copia no modifican original.

2. En C#, al hacer Punto copia = original, las dos variables hacen referencia al mismo objeto. Por eso si se modifica copia, también se observa el cambio cuando se utiliza original.

- ¿Qué es copia en C++ y en C#? ¿Es una copia independiente de original?

R: En C++ copia es un objeto independiente de original. En C# copia es una referencia al mismo objeto que original, por lo que no es una copia independiente.

## Actividad integradora de investigación

A. Predicción

- ¿Cuál será la salida final en la consola?

R: La salida muestra que el paso por valor no cambia la variable original, mientras que el paso por referencia y por puntero sí la cambian. También muestra que contador_estatico aumenta en cada llamada.

- Escribe la salida completa esperada.

```asm
--- Experimento con paso de parámetros ---
Valor inicial de val_A: 20
  -> Dentro de sumaPorValor, 'a' ahora es: 30
Valor final de val_A: 20

Valor inicial de val_B: 20
  -> Dentro de sumaPorReferencia, 'a' ahora es: 30
Valor final de val_B: 30

Valor inicial de val_C: 20
  -> Dentro de sumaPorPuntero, '*a' ahora es: 30
Valor final de val_C: 30

--- Experimento con variables estáticas ---
  -> Llamada a ejecutarContador. Valor de contador_estatico: 1
  -> Llamada a ejecutarContador. Valor de contador_estatico: 2
  -> Llamada a ejecutarContador. Valor de contador_estatico: 3
```
  
- Dibuja un mapa de memoria conceptual justo antes de que main finalice.

```asm
+--------------------------------+
|        SEGMENTO DE CÓDIGO      |
|                                |
| main()                         |
| ejecutarContador()             |
| sumaPorValor()                 |
| sumaPorReferencia()            |
| sumaPorPuntero()               |
+--------------------------------+
|     DATOS GLOBALES/ESTÁTICOS   |
|                                |
| contador_global = 100           |
| contador_estatico = 3           |
+--------------------------------+
|              HEAP              |
|                                |
| No se utiliza en este programa |
+--------------------------------+
|             STACK              |
|                                |
| val_A = 20                     |
| val_B = 30                     |
| val_C = 30                     |
| parámetros de las funciones    |
+--------------------------------+
```

- Compara la salida real con tu predicción.

R: La salida real debe coincidir con la predicción. val_A permanece en 20 porque se pasó por valor. val_B cambia a 30 porque se pasó por referencia y val_C cambia a 30 porque se pasó por puntero.

- ¿Qué demuestran las capturas sobre los diferentes tipos de paso por parámetros?

R: Las capturas demuestran que el paso por valor trabaja con una copia y no modifica la variable original. El paso por referencia y por puntero permiten modificar directamente la variable original.

- Explica con tus propias palabras el comportamiento de contador_estatico.

R: contador_estatico conserva su valor entre las llamadas a ejecutarContador. La primera vez vale 1, la segunda 2 y la tercera 3. Esto ocurre porque es una variable estática y solamente se inicializa una vez. Una variable local normal se crearía nuevamente cada vez que se llama a la función.
