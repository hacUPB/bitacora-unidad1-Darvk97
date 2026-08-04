# Sesión 2 #

# Actividad 2 – Experimento 1

Al ejecutar el programa observé que suma los valores 1 y 2, y luego guarda el resultado en la dirección de memoria 16.

- Valor almacenado en la dirección 16:3.
  
- ¿Por qué es ese valor?

  R: Porque el programa carga el número 1 en el registro D, luego le suma el número 2 y finalmente almacena el resultado en la memoria RAM 16.

- Instrucciones ejecutadas en cada ciclo Fetch-Decode-Execute:

1. Se lee @1 y se carga el valor 1.
2. D=A guarda 1 en el registro D.
3. Se lee @2.
4. D=D+A suma 1 + 2.
5. Se lee @16.
6. M=D almacena el resultado (3) en RAM 16.
7. El programa entra en un ciclo infinito con @END y 0;JMP.

## Cambios observados:
- El registro D cambia de 0 a 1 y luego a 3.
- La memoria RAM 16 cambia de 0 a 3.
- El contador de programa (PC) avanza hasta llegar al ciclo infinito.

# Actividad 2 – Experimento 2

## Programa

```asm
@5
D=A
@10
D=D+A
@20
M=D
(END)
@END
0;JMP
```

Al ejecutar el programa comprobé que la suma de 5 + 10 = 15 y el valor quedó correctamente almacenado en la dirección de memoria 20.

## Diferencia entre ROM y RAM

La memoria ROM almacena las instrucciones del programa y su contenido no cambia durante la ejecución. La memoria RAM almacena los datos y variables del programa, por lo que su contenido puede modificarse mientras el programa se está ejecutando.
