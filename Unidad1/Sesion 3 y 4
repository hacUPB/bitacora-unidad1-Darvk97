## Sesión 3 ##

## Actividad 3

1. Identifica una instrucción que use la ALU y explica qué hace.

R: La instrucción D=D-A utiliza la ALU para realizar una resta entre el contenido del registro D y el registro A. El resultado queda almacenado en D.

2. ¿Para qué sirve el registro PC?

R: El registro PC (Program Counter) guarda la dirección de la siguiente instrucción que la CPU debe ejecutar.

3. ¿Cuál es la diferencia entre @i y @READKEYBOARD?

R: @i hace referencia a una variable almacenada en memoria RAM, mientras que @READKEYBOARD hace referencia a una etiqueta del programa utilizada para realizar un salto.

4. Describe qué se necesita para leer el teclado y mostrar información en la pantalla.

R: Para leer el teclado se utiliza la dirección de memoria KBD, donde se almacena el código de la tecla presionada. Para mostrar información en la pantalla se escriben valores en las direcciones de memoria que comienzan en SCREEN.

5. Identifica un bucle en el programa y explica su funcionamiento.

R: El bucle comienza en la etiqueta (READKEYBOARD). El programa revisa continuamente si se presionó una tecla y, dependiendo del resultado, actualiza la pantalla y vuelve al inicio del ciclo.

6. Identifica una condición en el programa y explica su funcionamiento.

R: La instrucción D;JNE verifica si el contenido del registro D es diferente de cero. Si la condición se cumple, el programa salta a la etiqueta KEYPRESSED; de lo contrario continúa ejecutando las siguientes instrucciones.

# Actividad 4

## Programa

nasm
@5
D=M
@10
D=D-A
@MENOR
D;JLT

@0
D=A
@7
M=D
@FIN
0;JMP

(MENOR)
@1
D=A
@7
M=D

(FIN)
@FIN
0;JMP

## Observaciones

Durante la simulación comprobé que cuando el valor almacenado en la dirección 5 era menor que 10, la dirección 7 quedaba con el valor 1. Cuando el valor era igual o mayor que 10, la dirección 7 almacenaba el valor 0. El programa funcionó correctamente en ambos casos.

## Sesion 4 ##

Actividad 5
Programa
@1
D=A
@i
M=D

@0
D=A
@12
M=D

(LOOP)
@i
D=M
@6
D=D-A
@END
D;JEQ

@i
D=M
@12
M=D+M

@i
M=M+1

@LOOP
0;JMP

(END)
@END
0;JMP
Observaciones

El programa suma los números del 1 al 5 utilizando un ciclo. Al finalizar la ejecución, la dirección de memoria 12 contiene el valor 15.

Actividad integrada: Dibujando un punto
Ensamblador
@SCREEN
D=A
A=D
M=1

(END)
@END
0;JMP
C++
int pantalla[8192];
pantalla[0] = 1;
Observaciones

Al ejecutar el programa apareció un punto negro en la esquina superior izquierda de la pantalla.

Actividad integrada: Entrada y salida interactiva
C++
int posicion = 0;

while (true) {
    if (tecla == 'd')
        posicion++;

    if (tecla == 'i')
        posicion--;

  pantalla[posicion] = -1;
}

## Observaciones

La línea se desplazó hacia la derecha al presionar la tecla d y hacia la izquierda al presionar la tecla i.
