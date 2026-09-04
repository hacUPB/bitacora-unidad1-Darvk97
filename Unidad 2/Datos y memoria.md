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


# Sesión 3

## Actividad 6: Hola Objeto: creación de un objeto en el stack

### Programa

```cpp
#include <iostream>
using namespace std;

class Punto {
public:
    int x;
    int y;

    Punto(int _x, int _y) : x(_x), y(_y) {
        cout << "Constructor: Punto(" << x << ", " << y << ") creado." << endl;
    }

    ~Punto() {
        cout << "Destructor: Punto(" << x << ", " << y << ") destruido." << endl;
    }

    void imprimir() {
        cout << "Punto(" << x << ", " << y << ")" << endl;
    }
};

int main() {
    Punto p(10, 20);
    p.imprimir();

    return 0;
}
```

- ¿Cuál es la diferencia entre un constructor y un destructor?

R: El constructor se ejecuta cuando se crea un objeto y sirve principalmente para inicializarlo. El destructor se ejecuta cuando el objeto se destruye y sirve para liberar los recursos que pueda estar utilizando.

- ¿Cuál es la diferencia entre un objeto y una clase?

R: Una clase es como un molde que define las características y funciones que tendrá algo. Un objeto es una instancia creada a partir de esa clase.

- ¿Cuál es la diferencia entre el Punto de C++ y el de C#?

R: En C++ el objeto puede crearse directamente en el stack usando `Punto p(10, 20)`. En C# normalmente se crea usando `new`, como `Punto p = new Punto(10, 20)`, y la memoria del objeto se maneja automáticamente.

- ¿Qué es `p` en C++ y qué es `p` en C#?

R: En C++, `p` es un objeto de tipo `Punto`. En C#, `p` es una variable que contiene una referencia a un objeto `Punto`.

- ¿Dónde se almacena `p` en C++ y en C#?

R: En este ejemplo de C++, `p` se almacena directamente en el stack. En C#, la variable `p` contiene una referencia y el objeto creado con `new` se almacena en el heap.

- ¿Qué mostró el debugger sobre `p`? Según esto, ¿qué es un objeto en C++?

R: El debugger mostró que `p` contiene directamente los valores de sus atributos. Por ejemplo, se pueden observar los valores `10` y `20` en la memoria. Esto permite entender que un objeto en C++ es una región de memoria que contiene sus datos y sobre la que se pueden ejecutar sus funciones.

### Memoria

Al colocar un breakpoint en:

```cpp
Punto p(10, 20);
```

y revisar la dirección de `p` con `&p`, se puede observar en memoria cómo están guardados los valores.

Los valores son:

* `10` en hexadecimal = `0A`
* `20` en hexadecimal = `14`

Como Windows normalmente usa **little endian**, los bytes aparecen como:

```text
0A 00 00 00 14 00 00 00
```

Si se utilizara **big endian**, se guardarían de esta forma:

```text
00 00 00 0A 00 00 00 14
```

## Actividad 7: Objetos en el heap

### Programa

```cpp
#include <iostream>
using namespace std;

class Punto {
public:
    int x;
    int y;

    Punto(int _x, int _y) : x(_x), y(_y) {
        cout << "Constructor: Punto(" << x << ", " << y << ") creado." << endl;
    }

    ~Punto() {
        cout << "Destructor: Punto(" << x << ", " << y << ") destruido." << endl;
    }

    void imprimir() {
        cout << "Punto(" << x << ", " << y << ")" << endl;
    }
};

int main() {
    Punto pStack(30, 40);
    pStack.imprimir();

    Punto* pHeap = new Punto(50, 60);
    pHeap->imprimir();

    delete pHeap;

    return 0;
}
```

- ¿Cuál es la diferencia entre los objetos creados en el stack y los objetos creados en el heap?

R: El objeto del stack se crea directamente y se destruye automáticamente cuando termina su alcance. El objeto del heap se crea usando `new` y debe liberarse usando `delete`.

- ¿`pStack` es un objeto o una referencia?

R: `pStack` es un objeto de tipo `Punto`. El objeto está almacenado directamente en el stack.

- ¿`pHeap` es un objeto o una referencia? Si es una referencia, ¿a qué?

R: `pHeap` es un puntero, no una referencia. Es una variable que almacena la dirección de un objeto `Punto` que está en el heap.

- Al colocar un breakpoint en `&pHeap` y comparar el contenido de Memory 1 con el valor de `pHeap` en Locals, ¿qué se observa?

R: Se observa que en la dirección de `pHeap` está guardado el valor de la dirección del objeto que está en el heap. Por eso el valor que aparece en Memory 1 corresponde a la dirección que muestra `pHeap` en Locals.

## Actividad 8: Funciones y objetos en C++

### Programa

```cpp
#include <iostream>
#include <string>
using namespace std;

class Punto {
public:
    string name;
    int x;
    int y;

    Punto(string _name, int _x, int _y) : name(_name), x(_x), y(_y) {
        cout << "Constructor: Punto " << name << " (" << x << ", " << y << ") creado." << endl;
    }

    ~Punto() {
        cout << "Destructor: Punto " << name << "(" << x << ", " << y << ") destruido." << endl;
    }

    void imprimir() {
        cout << "Punto " << name << "(" << x << ", " << y << ")" << endl;
    }
};

void cambiarNombre(Punto p, string nuevoNombre) {
    p.name = nuevoNombre;
}

int main() {
    Punto original("original", 70, 80);

    original.imprimir();

    cambiarNombre(original, "cambiado");

    original.imprimir();

    return 0;
}
```

- ¿Qué ocurre después de llamar a `cambiarNombre`? ¿Por qué el destructor dice "cambiado"?

R: Cuando se llama a `cambiarNombre`, se crea una copia de `original` llamada `p`. Dentro de la función se cambia el nombre de esa copia a `"cambiado"`. Cuando termina la función, la copia `p` se destruye y por eso el destructor muestra `"cambiado"`.

- ¿Por qué `original` todavía existe?

R: Porque `original` y `p` son objetos diferentes. `p` es una copia de `original`, por lo que cambiar o destruir `p` no destruye `original`.

- ¿Dónde están `original` y `p`? ¿Son el mismo objeto?

R: Los dos son objetos locales y en este ejemplo se encuentran en el stack. No son el mismo objeto. `p` es una copia de `original`.

### Pasando el objeto por referencia

Se cambia la función por:

```cpp
void cambiarNombre(Punto& p, string nuevoNombre) {
    p.name = nuevoNombre;
}
```

- ¿Qué ocurre ahora y por qué?

R: Ahora sí se cambia el nombre de `original`. Esto pasa porque `p` es una referencia al mismo objeto `original`, por lo que no se crea una copia.

- ¿Qué pasa con el destructor?

R: El destructor de la copia ya no aparece porque no se crea una copia. El destructor de `original` se ejecuta cuando `original` sale de su alcance al terminar `main`.

### Pasando el objeto por puntero

Se cambia la función por:

```cpp
void cambiarNombre(Punto* p, string nuevoNombre) {
    p->name = nuevoNombre;
}

int main() {
    Punto original("original", 70, 80);

    original.imprimir();

    cambiarNombre(&original, "cambiado");

    original.imprimir();

    return 0;
}
```

- ¿Qué ocurre ahora y por qué?

R: Ahora también se cambia el nombre de `original`. Se envía su dirección usando `&original` y el puntero `p` recibe esa dirección. Con `p->name` se puede modificar el objeto original.

- ¿Cuál es la diferencia entre pasar un objeto por valor, referencia y puntero?

R: Al pasar por valor se crea una copia del objeto, por lo que los cambios no afectan al original. Al pasar por referencia se trabaja directamente con el objeto original. Al pasar por puntero se envía la dirección del objeto y también se puede modificar el original usando `->`.

R: En resumen:

* **Por valor:** se crea una copia.
* **Por referencia:** se trabaja directamente con el objeto original.
* **Por puntero:** se pasa la dirección del objeto original.

