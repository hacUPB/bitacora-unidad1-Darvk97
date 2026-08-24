* Sesión 5 *
Programa en ensamblador

// Suma 1 + 2 + ... + 100

@sum
M=0          // sum = 0

@i
M=1          // i = 1

(LOOP)
    @i
    D=M
    @100
    D=D-A
    @END
    D;JGT      // Si i > 100 termina

    @i
    D=M
    @sum
    M=M+D      // sum = sum + i

    @i
    M=M+1      // i++

    @LOOP
    0;JMP

(END)
    @END
    0;JMP
Conclusión

Los ciclos while y for generan prácticamente el mismo código en ensamblador. La única diferencia está en cómo se escriben en C++, pero al traducirlos ambos tienen una inicialización, una condición, el cuerpo del ciclo y el incremento. En ensamblador esa estructura es igual.

Sesión 6. Punteros
Programa 1
C++
int a = 10;
int *p;
p = &a;
*p = 20;
Ensamblador
// a = RAM[16]
// p = RAM[17]

@10
D=A
@16
M=D          // a = 10

@16
D=A
@17
M=D          // p = &a

@17
A=M
M=20         // *p = 20
Reflexión

El puntero guarda la dirección de la variable a. Cuando uso A=M, el procesador va a esa dirección y puedo modificar directamente el valor de a.

Programa 2
C++
int a = 10;
int b = 5;
int *p;

p = &a;
b = *p;
Ensamblador
// a = 16
// b = 17
// p = 18

@10
D=A
@16
M=D          // a = 10

@5
D=A
@17
M=D          // b = 5

@16
D=A
@18
M=D          // p = &a

@18
A=M
D=M          // D = *p

@17
M=D          // b = *p
Reflexión

En este caso el puntero no escribe sino que lee el contenido de a. Al final b cambia de 5 a 10 porque copia el valor almacenado en la dirección apuntada.
